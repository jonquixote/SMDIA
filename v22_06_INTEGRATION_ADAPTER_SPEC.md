# Integration Adapter Specification

**Project:** Social Distance as Interface  
**Version:** v22  
**Owner:** Engineering / Security / Compliance  
**Readers:** Engineers, security, compliance, partner/platform reviewers  
**Authority level:** Binding specification  
**Changes require:** Engineering + security approval; compliance review for new capability/provider  
**Review cadence:** Per adapter release, policy change, or material external API change  
**Conflicts resolved by:** `00_PRODUCT_CONSTITUTION.md`  
**Last cross-document consistency review:** 2026-07-27

## Purpose

Adapters are optional, replaceable integrations for identity linking, candidate import, public-content reference, cross-post export, or payment links. They do not own canonical records or modify native authorization without explicit native action.

## Capability Manifest

Every adapter publishes a versioned manifest containing supported capabilities, schemas, consent-language version, policy-compliance status, rate limits, retention behavior, deprecation/migration date, known limitations, and last successful sync state.

## Data-Minimization Matrix

| Capability | Data requested | Stored? | Retention | User-visible use | Permission |
|---|---|---|---|---|---|
| Identity link | External ID, handle, verification proof | Yes, minimum | Disconnect + published retention window | Verified linked identity | Explicit link |
| Candidate import | Relationship identifiers + provenance | Yes, candidate only | Until removal/disconnect/retention window | Suggested native follows | Explicit import |
| Public-content reference | External post ID, URL, author, minimal preview | Minimal reference | Source terms + policy | Context/link preview | User-selected |
| Cross-post export | Native public payload + destination receipt | Outbound receipt/audit only | Audit retention window | Distribution status | Per-write acknowledgment |
| Payment link | Provider identity/status needed for link | Minimum | Link lifetime + retention | External payment option | Explicit link |

Private content, private audience membership, bridge topology, and private metadata never enter an adapter request or export queue (`CONST-TRUST-001`, `CONST-GRAPH-003`).

## User-Controlled Import Modes

- Preview only: show candidates; create no native edges
- Confirm individually
- Confirm selected in bulk
- Link only: verify external identity; import no graph data
- One-time import
- Ongoing sync: off by default; visible last-sync timestamp and pause/disconnect control
- Disconnect and purge adapter-derived candidate data, subject to published audit/legal retention

Imported candidates show source, confirmation state, last refresh, removal option, and conversion action. They never silently become native follows, audience recipients, bridges, reputation, governance, or economic edges.

## Synchronization Rules

- Imports are user-triggered or explicitly scheduled only after opt-in.
- External relationship disappearance marks a candidate stale; it does not delete a confirmed native edge.
- Candidate provenance remains historical only as long as stated by retention policy.
- External handle/account changes update only through permitted refresh and remain visibly sourced.
- Public content references state whether they are live, cached, or snapshotted.
- Disconnect removes credentials/stops sync; UI removal, audit preservation, and candidate-data purge follow declared policy.

## Credentials and External Writes

Scopes are minimum necessary; read/import and write/export scopes are separate; tokens are encrypted, rotated, and access-logged. External writes require native public classification, destination disclosure, user acknowledgment, idempotency, status visibility, retry/cancel control, and receipt logging.

## Failure Behavior

| Failure | Required behavior |
|---|---|
| Import unavailable | Native product continues; show stale/last-refresh state; pause sync |
| Export unavailable | Native public post remains; queue/retry only with visible cancel option |
| Credential revoked | Stop capability; relink only on user request |
| API/policy change | Disable affected capability safely; retain native data |
| Provenance mismatch | Quarantine candidate data; require user confirmation |
| Suspected compromise | Revoke tokens, halt traffic, investigate; native authorization unaffected |

## First Capability Decision

Phase 0 selects **one first adapter capability**, not a full platform bundle, using onboarding value, compliance cost, privacy risk, support burden, and reversible implementation as criteria:

1. Contact import
2. Linked public identity verification
3. User-approved cross-post export

No adapter is assumed to provide import, identity, and write capability at once.

## AT Protocol / Bluesky

AT Protocol/Bluesky is one possible first adapter. Its OAuth/PDS/read/write/API-specific implementation lives in a versioned appendix maintained with adapter code. It cannot alter the native-first contract or upgrade imported data into native rights.

## Changelog

- **v22:** Adds import modes, data-minimization matrix, lifecycle/sync semantics, capability manifest/versioning, and first-capability decision discipline.