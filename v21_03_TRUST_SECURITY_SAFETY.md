# Trust, Security, and Safety Specification

**Project:** Social Distance as Interface  
**Version:** v21  
**Owner:** Security / Build Lead  
**Readers:** Engineering, security, operations, legal, moderation  
**Controls:** Data boundaries, threat model, access controls, safety operations, test plan  
**Depends on:** `00_PRODUCT_CONSTITUTION.md`, `02_PRODUCT_PRD.md`  
**Links:** Adapter details in `06_INTEGRATION_ADAPTER_SPEC.md`

## Purpose

Make the product’s promises mechanically true: private content stays private, audience delivery is honest, graph topology is not leaked, external writes are consented, and safety operations have defined authority and evidence paths.

## Data Classification

| Class | Examples | Minimum handling |
|---|---|---|
| Private content | Private posts, private notes, attachments | Encrypted at rest; strict authorization; no external transmission |
| Social metadata | Audience size, invitation state, interaction time | Minimized, access controlled, excluded from third-party analytics by default |
| Graph topology | Bridge paths, mutual relationships, degree estimates | Coarsened, consent-gated, never enumerable |
| Public content | Open-network posts, externally cross-posted records | Public policy; destination and provenance retained |
| Financial data | Payments, payouts, splits, tax records | Segregated access, audit logging, compliance controls |
| Security data | Sessions, recovery events, privileged-access logs | Protected, retention-controlled, reviewable |

## Architecture Boundaries

- Native identity, graph, content, authorization, community, payment, and policy records are canonical.
- Private content is stored server-private and encrypted at rest; it is not E2EE at MVP.
- Adapter credentials and adapter write paths are isolated from private-content services.
- Imports enter as provenance-labeled candidate records; no imported edge grants authorization or rights automatically.
- Cross-posting operates only on explicit public records and requires logged user consent.

## Required Invariants

| Invariant | Automated / operational verification |
|---|---|
| No private federation | Egress controls, contract tests, payload scanning, integration-test assertions |
| Honest audience count | Compose state derived only from active authorized recipients; invitees distinct |
| Explicit authorization | Permission checks require native audience edge and post snapshot |
| Historical access protection | Authorization query tests reject post-creation additions except valid token exception |
| Revocation | Token/session/access checks invalidate on remove, block, deletion, expiry |
| Consented external write | Publish endpoint requires destination acknowledgment record |
| No topology leak | Privacy thresholds, response filters, red-team graph-inference tests |
| Ranking separation | Ranking service has no authority to modify authorization/rights |
| Auditable privilege | Immutable/append-only access logs, review process, least-privilege roles |
| Defined deletion | Job logs and policy evidence cover live store, backups, holds, and adapter copies |

## Threat Model

### Primary threats

- Accidental private-content federation, cross-post, notification preview, attachment URL leak, or analytics leak
- Graph/topology inference through exact reach estimates, degree counts, bridge paths, or small communities
- Invitation forwarding, farming, impersonation, duplicate accounts, malicious invite copy, and pre-signup harassment
- Session theft, account takeover, unsafe recovery, and device compromise
- Insider/support/operator/moderator access beyond need
- Abuse reports exposing more private content than necessary
- Legal demands, subpoenas, legal holds, and retention ambiguity
- Backup, logging, error-reporting, and disaster-recovery persistence
- Adapter credential compromise, API behavior changes, or unauthorized external writes
- Targeted harassment, brigades, community operator abuse, and payment fraud

### Non-preventable risks communicated honestly

Recipients can screenshot, copy, or describe private content. The system can constrain retrieval and forwarding but cannot make viewed content unseen. Product copy and reporting flows must not imply otherwise.

## Identity, Sessions, and Recovery

- Native identity is primary; external linked identities are proofs/adapters.
- Handle changes, account linking/disconnection, duplicate accounts, impersonation, and organization verification have documented workflows.
- Session list, remote logout, risky-login notification, and recovery challenge requirements ship before broad discovery.
- Recovery cannot silently rebind a recipient-bound invitation token to an unverified account.

## Private Audience and Invite Security

- Invitation tokens are random, unique, recipient-bound, expiration-controlled, and revocable.
- Token redemption verifies recipient identity before granting trigger-post access.
- Links are rate-limited and monitored for unusual forwarding.
- Invitees can block/report prior to account creation.
- Removal/block/deletion invalidates unused tokens immediately.
- Trigger-post exception is narrowly scoped: it grants exactly the triggering post and future authorized posts, never a private back catalog.

## Bridge-Graph Safety

- Bridge consent is opt-in and scoped by category/community/context.
- No exact intermediary names, degree counts, or graph paths without all required consents.
- Minimum crowd thresholds suppress reach estimates and social-context labels in sparse graphs.
- The system prevents graph enumeration through search, repeated querying, and differential responses.
- Bridge consent is separate from follows, private audiences, interaction, and community membership.

## Moderation and Safety Operations

### Roles

- **Platform safety team:** platform-wide enforcement, severe incident response, appeals escalation
- **Community operators:** charter-limited community moderation; no default access to private posts or audience lists
- **Report reviewer:** minimum-necessary evidence access, time-bound, audited
- **Security/build lead:** incident containment, access review, root cause

### Required processes

- Block, mute, report, rate limiting, invitation abuse controls, and targeted-harassment detection
- Defined evidence bundle for private reports, preservation rules, and reviewer access
- Cross-surface enforcement policy for native Open posts and adapter-cross-posted public content
- Response-time SLA, escalation ladder, appeal path, and incident communications template
- Operator training, replacement process, and audit review

## Deletion, Retention, and Legal Process

The policy distinguishes live data, encrypted backups, logs, legal holds, and external copies.

- Account deletion removes live private content and revokes invitations according to documented deletion jobs.
- Encrypted backups and disaster-recovery copies follow published retention windows.
- Legal holds pause deletion only to the documented scope and are logged.
- External cross-posts are governed by destination policy and may persist after native deletion; users see this at deletion time.
- Exports include the user’s content, policy history, invitations, audience records, and eligible moderation/economic records.

## Incident Severity

| Severity | Example | Response |
|---|---|---|
| SEV-0 | Confirmed broad private-content exposure | Stop affected writes/reads, executive/security incident, user notification plan |
| SEV-1 | Unauthorized single-user private access or topology exposure | Contain, investigate, remediate, assess notification |
| SEV-2 | Invite abuse pattern, security-control bypass attempt | Rate-limit/disable path, investigate, release fix |
| SEV-3 | UX confusion or non-sensitive policy defect | Triage, patch, monitor |

## Security Test Plan

- Unit tests for policy evaluator and state transitions
- Integration tests for post snapshots, invite redemption, revocation, deletion, and external-write isolation
- Property/fuzz tests for authorization and token flows
- Red-team graph-inference and bridge-leak testing
- Dependency, credential, and egress scanning
- Privileged-access log reviews
- Incident tabletop exercises for private leak, adapter compromise, and targeted harassment

## Changelog

- **v21:** Separated from v20; adds data classification, operational role model, severity scheme, and a dedicated test plan.