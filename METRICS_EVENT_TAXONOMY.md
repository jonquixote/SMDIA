# Metrics and Event Taxonomy

**Project:** Social Distance as Interface  
**Phase:** 0 hardening pass v2  
**Authority:** Measurement contract; thresholds lock in Launch Scorecard v1 by Day 14  
**Owners:** Product, Research, Safety, Security, Operations, Finance

## Event Standard

Completed actions use past-tense snake_case names. Every event uses stable internal object IDs, enumerated properties, ISO-8601 UTC timestamps, and explicit privacy classification.

```json
{
  "event_name": "private_post_published",
  "event_id": "uuid",
  "occurred_at": "ISO-8601 UTC",
  "actor_id": "pseudonymous_internal_id",
  "session_id": "pseudonymous_internal_id",
  "schema_version": 1,
  "client_version": "string",
  "surface": "compose",
  "policy_schema_version": "uuid_or_version",
  "privacy_class": "restricted_metadata"
}
```

`community_id` is attached only when necessary for an authorized community-scoped metric. Never collect private plaintext, attachment URLs, raw invite tokens, exact bridge paths, or user-visible names. Add `policy_id`, `policy_snapshot_id`, `policy_schema_version`, `event_schema_version`, `evaluator_version`, `authorization_outcome`, `experiment_assignment_id`, `data_processing_region`, `source_channel`, and `is_test_account` where relevant.


## Stream Definitions

| Stream | Examples | Primary access |
|---|---|---|
| Product analytics | `private_post_published`, `delivery_count_viewed`, `introduction_accepted` | Product/research, pseudonymized |
| Security audit | `private_post_access_denied`, privileged access, token revocation, suspicious recovery | Security, restricted |
| Consent/compliance receipts | `external_write_acknowledged`, rights consent, bridge-consent changes | Security/legal, append-only |
| Moderation cases | `report_created`, evidence, action, appeal, `invite_reported` | Safety, role-based |
| Observability/data quality | schema rejects, duplicate events, evaluator mismatch, pipeline lag | Engineering/data platform |
## Data Streams

| Stream | Purpose | Access/retention |
|---|---|---|
| Product analytics | Adoption, comprehension, retention, efficacy | Pseudonymized; minimum metadata; restricted analytics access |
| Security/audit logs | Denials, token events, staff access, suspicious behavior, incidents | Tightly controlled, immutable where needed |
| Financial ledger | Payments, fees, payouts, refunds, entitlements | Reconciled; finance-controlled; legally retained |
| Moderation case system | Reports, evidence, actions, appeals | Case-controlled; role-based retention |

## Product Analytics Events

`activation_completed`, `private_post_composer_opened`, `private_audience_selected`, `delivery_count_viewed`, `private_post_published`, `private_post_viewed`, `invite_created`, `invite_shared`, `invite_opened`, `invite_redeemed`, `bridge_consent_changed`, `context_discovery_impression`, `introduction_requested`, `introduction_accepted`, `introduction_declined`, `mutual_follow_created`, `substantive_reply_qualified`, `project_action_completed`, `export_requested`, `export_completed`, `payment_attempted`, `payment_completed`, `payment_refunded`, `payout_completed`.

Properties are enumerated/bucketed: audience type, active-count bucket, invitee-count bucket, policy version, mode, discovery mode, time policy, response latency bucket, payment result, fee version. See implementation schema registry for per-event fields.

## Security, Audit, and Data-Quality Events

`private_post_access_denied`, `invite_verified`, `invite_revoked`, `invite_reported`, `invite_blocked`, `external_write_acknowledged`, `external_write_result`, `report_created`, `report_resolved`, `safety_incident_confirmed`, `topology_protection_triggered`, `event_schema_rejected`, `event_duplicate_detected`, `metric_pipeline_lag_detected`, `policy_evaluator_version_mismatch_detected`, `analytics_consent_changed`, `data_deletion_propagation_completed`.

A `policy_evaluator_version_mismatch_detected` is a security/product integrity alert: compose preview, authorization, feed, or distribution evaluated incompatible policy versions.

## Balanced Scorecard

| Dimension | Metric | Formula |
|---|---|---|
| Private-loop retention | Week-4 private retention | Activated cohort active in private view/post in week 4 / activated cohort |
| Relationship formation | Relationship formation rate | WAU with accepted introduction, durable mutual follow, substantive reciprocal exchange, or completed project action / WAU |
| Economic validation | Completed support rate | Non-refunded completed support/payout events / eligible attempts |
| Comprehension | Audience comprehension | Tested users correctly identifying current audience and discovery status / tested users |
| Invite quality | Invite nuisance rate | Unique invitees blocking/reporting / valid delivered invites |
| Operations | Report SLA compliance | Reports resolved within category SLA / eligible resolved reports |
| Financial integrity | Ledger accuracy | Reconciled eligible ledger records / sampled or total eligible records |

A second private post is a **retention** signal, not interpersonal relationship formation.

## Incident Classes and Gates

| Code | Meaning | Gate |
|---|---|---|
| P0_PRIVATE_EGRESS | Private content/metadata sent to external endpoint | Immediate hard stop |
| P0_UNAUTHORIZED_PRIVATE_READ | Unauthorized retrieval of private content | Immediate hard stop |
| P0_AUDIENCE_POLICY_BYPASS | Evaluator grants access outside intended audience | Immediate hard stop |
| P0_PRIVILEGED_ACCESS_VIOLATION | Insider access outside approved audited path | Immediate hard stop |
| P0_CRITICAL_CREDIBLE_VULNERABILITY | A critical, realistically exploitable flaw with no confirmed production exposure yet | Freeze affected surface until mitigated |
| P1_POLICY_EVALUATOR_MISMATCH | Preview and enforcement use incompatible semantics or snapshots | Block feature rollout; investigate scope |
| P1_TOPOLOGY_DISCLOSURE | Confirmed hidden path/intermediary/degree disclosure | Disable affected discovery feature |
| P1_UNSAFE_RECOVERY | Confirmed account recovery compromise | Pause affected recovery/access flow |
| P1_ADAPTER_UNAUTHORIZED_WRITE | Adapter writes without valid consent/public classification | Disable adapter write capability |
| P2_INVITE_ABUSE_PATTERN | Trend of abusive/spam invitations | Tighten limits; pause growth experiment |
| P2_REPORT_SLA_FAILURE | Report response below threshold | Add coverage or pause expansion |

Recipient screenshots, voluntary forwarding after legitimate viewing, and non-sensitive metadata issues without unintended disclosure are not P0 private-exposure incidents, though they may warrant UX, safety, or education work.

## Day-14 Scorecard Requirement

Each metric must have threshold, baseline/sample size, query owner, data-quality checks, decision authority, cadence, and miss response. Metric changes require a decision record and preserved historical comparability.