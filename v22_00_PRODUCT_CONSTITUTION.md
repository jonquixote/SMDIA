# Product Constitution

**Project:** Social Distance as Interface  
**Version:** v22  
**Owner:** Founder  
**Readers:** All contributors, advisors, operators, and partners  
**Authority level:** Constitutional  
**Changes require:** Explicit founder decision; security and legal review for trust/economic changes  
**Review cadence:** Monthly, before every launch gate, and after any SEV-0/SEV-1 incident  
**Conflicts resolved by:** This document  
**Last cross-document consistency review:** 2026-07-27

## Purpose and Mission

This Constitution defines the durable bargain between the platform and its users: social reach is legible and enforceable; user relationships and value are not platform property; and growth, ranking, payout, governance, and integrations cannot quietly weaken those commitments.

> **Social networks force people to choose between broadcasting and disappearing. This network gives every post a legible, enforceable distribution policy that its author chooses.**

The system controls access and platform distribution. It cannot prevent a recipient from screenshotting, copying, or describing content they have viewed.

## Precedence

The Constitution governs product, engineering, operations, economic policy, and integration decisions. A lower-level document may add specificity but cannot weaken a constitutional guarantee. If a lower-level specification conflicts with this document, it must be revised or obtain a dated constitutional amendment.

## Non-Negotiable User Rights

- Users choose an understandable policy for immediate audience, later discovery, distribution, time, destination, and optional economic terms.
- A person is never represented as able to view a private post before authorization is active.
- Following, importing, interacting, paying, or joining a community never silently grants private access, bridge consent, governance rights, or economic entitlement.
- Private content never reaches an external endpoint.
- Users can export their own content, records, and consent-respecting relationship metadata; they do not own other people’s private data.
- External writes require destination disclosure and affirmative acknowledgment.
- Platform extraction is governed by a disclosed fee policy, transparent value-flow rules, and a binding cap or amendment process finalized before public economic promises are made.
- No core ranking, payout, governance, or growth mechanism may optimize solely for impressions, time spent, raw engagement, follower count, invitations sent, or transactions generated without associated quality, consent, safety, and fraud-resistance measures.

## Graph and Authorization Doctrine

### CONST-GRAPH-001 — Explicit Graphs

The system has five distinct graphs: follow, private audience, interaction, discovery bridge, and economic contribution. No graph edge silently creates an edge in another graph.

### CONST-GRAPH-002 — Follow Is Not Authorization

A follow means “I want to see this person.” It never grants private-audience access, bridge consent, reputation, governance rights, or economic rights.

### CONST-GRAPH-003 — Distance Is Not Permission

Graph distance never independently authorizes distribution. Eligible reach is evaluated as:

\[
\text{EligibleReach} = \text{AuthorPolicy} \cap \text{RecipientConsent} \cap \text{RelationshipContext} \cap \text{CommunityRules} \cap \text{SafetyConstraints}
\]

### CONST-BRIDGE-001 — Consent-Qualified Bridging

A person may function as a discovery bridge only through explicit, scope-specific consent. Bridge use never implies endorsement or permits intermediary identity disclosure without all necessary consents and anonymity thresholds.

### CONST-TRUST-001 — Honest Delivery

Compose and notifications distinguish active authorized recipients from invitees or later-eligible people. A policy preview may be coarsened for privacy but may never overstate present or future eligibility.

### CONST-TRUST-002 — Snapshot Authorization

Private posts use a post-time authorization snapshot. People added later cannot retrieve older posts except through the narrowly defined token-bound trigger-post invitation exception.

### CONST-TRUST-003 — Revocation

Removal, blocking, deletion, expiry, or failed recipient verification revoke future authorization and unused invitation access immediately. They cannot make already viewed content unseen.

## Economic and Anti-Extraction Doctrine

### CONST-ECON-001 — Legible Extraction

Fees, deductions, payout terms, and value-flow policy are disclosed, versioned, and auditable. Customer/creator funds payable to creators or collaborators are liabilities, not company surplus.

### CONST-ECON-002 — Creator Rights

Creators retain copyright by default. The platform receives only the limited license necessary to host, secure, process, display, and distribute content according to selected policy. The platform receives no blanket AI-training, advertising, or unrelated commercial-reuse license.

### CONST-PORT-001 — Consent-Respecting Portability

Users export their relationship records and permitted opt-in contact/channel data, not others’ private identities, contact details, or undisclosed graph topology.

### CONST-METRIC-001 — No Metric Gaming

Every core growth, ranking, payout, or governance metric has quality, consent, safety, and fraud-resistance companion measures. A metric cannot be used as a sole optimization target when it can be raised by unwanted exposure, abuse, manipulation, or extraction.

## Canonical System Rule

Native identity, graph, content, visibility policy, community membership, payment entitlement, and governance records are canonical. External imports are candidate data; external cross-posts are outbound copies. Adapter loss degrades convenience, not core operation.

## Governance and Amendment Process

| Change class | Meaning | Approval and notice |
|---|---|---|
| Clarification | Wording changes with no behavior change | Document owner review and changelog |
| Policy change | Operating/default change that honors all constitutional rules | Relevant owner review; product/security review; advance notice when materially user-facing |
| Constitutional amendment | Changes protected term, right, invariant, anti-goal, canonical rule, or economic guarantee | Founder decision; security + legal review where applicable; public version history; affected-stakeholder review; waiting period before effective date unless needed for active safety/legal emergency |

Every constitutional amendment records: problem, alternatives considered, decision, owner, date, migration impact, affected users, and notice path. No formal democracy is presumed before a viable participant base exists, but no foundational bargain may be quietly rewritten.

## Interpretation and Conflict Resolution

Questions are resolved by: (1) the most protective reading of a stated user right, (2) the rule preventing irreversible privacy/financial harm, then (3) founder, security, and legal review. Approved exceptions are time-bound, documented, and reviewed after use.

## Changelog

- **v22:** Adds stable constitutional IDs, precedence, amendment classes, no-metric-gaming rule, creator-rights default, and governance process.