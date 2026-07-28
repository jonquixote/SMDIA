# Integration Adapter Specification

**Project:** Social Distance as Interface  
**Version:** v21  
**Owner:** Engineering / Security / Compliance  
**Readers:** Engineers, security reviewers, compliance, partner/platform reviewers  
**Controls:** Adapter contract, provenance, credentials, failure behavior, external-write isolation  
**Depends on:** `00_PRODUCT_CONSTITUTION.md`, `03_TRUST_SECURITY_SAFETY.md`  
**Links:** Product behavior in `02_PRODUCT_PRD.md`

## Purpose

Define a generic, replaceable interface for external identity/import/distribution integrations. Adapters improve onboarding and reach; they never become the canonical source for identity, graph, content, visibility, economic rights, or governance.

## Adapter Contract

An adapter may expose any subset of the following capabilities:

| Capability | Description |
|---|---|
| Identity link | Verify or link an external account to native identity |
| Contact/relationship import | Import candidate relationships with provenance |
| Public content reference/import | Reference public external content under permitted terms |
| Cross-post export | Write a user-approved native public record to an external destination |
| Payment link | Attach/verify an external payment destination where allowed |

Adapters must declare supported capabilities, data fields, freshness, revocation behavior, rate limits, compliance requirements, and failure mode.

## Canonical Data Rules

- Native records remain canonical.
- Imported relationships are candidate edges with provenance, not native follows or permissions.
- An imported edge cannot grant private-audience access, bridge consent, reputation, governance, or economic entitlement.
- External content is a reference/copy with provenance, not a replacement for native content.
- Cross-posts are outbound copies of explicit native public records.
- Adapter loss never removes native relationships, content, authorization, policies, earnings records, or governance history.

## Candidate-Edge Lifecycle

Each imported candidate edge records:

- Source adapter and external identifier
- Import timestamp and last refresh
- Consent/confirmation state
- Matching confidence and user-visible explanation where relevant
- Removal/disconnect option
- Conversion event to native follow or other explicit native edge

The UI never presents imported candidates as trusted/private/endorsed relationships by default.

## Credential and OAuth Requirements

- Credentials are scoped to the minimum required capabilities.
- Read/import and write/export scopes are separately requested and revocable.
- Tokens are encrypted, rotated, logged for use, and never exposed to client telemetry.
- External write scopes are requested only when the user enables the relevant action.
- Disconnect revokes local credentials and stops synchronization; external revocation behavior is documented per adapter.

## External-Write Isolation

Only native records classified as public and explicitly selected for a destination may enter an adapter write queue.

Before each external write, the system records:

- User identity
- Native record ID
- Destination adapter/account
- Publicness disclosure version
- User acknowledgment timestamp
- Retry/idempotency key
- Result, external identifier, and failure reason

Private content, private metadata, private audience membership, internal graph topology, and private attachment URLs are structurally blocked from all adapter write paths.

## Data Retention and Deletion

- Adapter-derived data has provenance and retention rules.
- Disconnect removes credentials and stops new import/export.
- Native content deletion does not promise deletion of external copies; the UI states destination-specific behavior.
- Exports distinguish native records from adapter references.
- Adapter webhooks/events are filtered to the minimum data necessary and cannot modify native permissions without explicit native user action.

## Failure and Degradation

| Failure | Required behavior |
|---|---|
| Adapter read/import unavailable | Native product continues; show stale/last-refresh state; pause sync |
| Adapter write unavailable | Native public post remains; queue/retry only with user-visible status and cancellation option |
| Credential revoked | Stop capability; prompt relink only if user requests it |
| API policy change | Disable affected capability safely; retain native data |
| Provenance mismatch | Quarantine candidate data; require confirmation |
| Adapter compromise suspicion | Revoke tokens, halt traffic, investigate; no effect on native authorization |

## Adapter Security Tests

- Scope and token storage tests
- Egress allowlist and payload inspection
- Verify no private record can enter export queue
- Idempotent cross-post/retry tests
- Disconnect/revocation tests
- Candidate-edge provenance and conversion tests
- Rate-limit/backoff tests
- Failure-mode and stale-data UI tests
- Compliance review per adapter

## Adapter: AT Protocol / Bluesky

Initial adapter capability assessment may include:

- Linked identity verification
- Public follow/content candidate import where permitted
- Optional public content references
- User-approved cross-post export via appropriate authentication

AT Protocol/Bluesky-specific details—OAuth flow, PDS write behavior, read APIs, rate limits, content policy, and compliance requirements—belong in a versioned implementation appendix maintained with the adapter code. They must not alter the native-first contract.

## Future Adapter Examples

- ActivityPub/Mastodon
- Email contacts
- Phone contacts
- Creator-platform imports
- Payment-link providers

Each uses this contract and receives its own compliance/security appendix.

## Changelog

- **v21:** New standalone adapter contract extracted from v20 to prevent integration concerns from competing with core product doctrine.