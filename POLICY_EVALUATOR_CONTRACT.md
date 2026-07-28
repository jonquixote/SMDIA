# Policy Evaluator Contract

**Project:** Social Distance as Interface  
**Version:** v1.0 — Ready to freeze after implementation review  
**Owners:** Product, Engineering, Security  
**Authority:** Binding source of truth for policy authorization and reach decisions  
**Changes require:** Product, engineering, and security approval; safety/legal approval where applicable  
**Review:** Before beta, any policy-schema or evaluator-semantic change, and after relevant P0/P1 incident

## Purpose

The Policy Evaluator is the canonical, fail-closed decision engine for content reach and related rights. It governs retrieval, discovery, reshare, introductions, external writes, commerce access, invitations, notification, export, reporting, moderation review, deletion, and audit-history access.

A graph distance, follow, imported edge, interaction, community membership, payment, or ranking score never independently authorizes a protected action. Compose preview and enforcement must use compatible policy snapshots and evaluator semantics.

## Canonical Objects

```text
PostReachPolicy
- policy_id
- policy_schema_version
- immediate_audience_rule
- discovery_rule
- distribution_rule
- reshare_policy
- time_rule
- destination_rule
- entitlement_rule
- economic_rule
- rights_rule
- safety_constraints

PolicySnapshot
- policy_snapshot_id
- policy_id
- policy_schema_version
- serialized_policy
- created_at

PublicationSnapshot
- publication_snapshot_id
- post_id
- policy_snapshot_id
- audience_snapshot_id
- authorization_timestamp
- applicable_community_charter_version
- created_at
```

| Object/field | Meaning |
|---|---|
| `policy_id` | Immutable identifier for a specific policy instance |
| `policy_schema_version` | Version of policy data model |
| `evaluator_semantics_version` | Version of evaluator interpretation/logic |
| `policy_snapshot_id` | Immutable published policy snapshot bound to post |
| `audience_snapshot_id` | Immutable published audience authorization state |
| `publication_snapshot_id` | Immutable record joining post, policy snapshot, audience snapshot, authorization time, and charter version |
| `entitlement_rule` | Who may access: free, purchased, subscribed, gifted, or community-granted |
| `economic_rule` | Pricing, fees, payout allocation, splits, refunds, and payment terms |
| `distribution_rule` | Which channels are enabled: recommendation, reshare, introduction, external copy |
| `reshare_policy` | Constraints within enabled reshare: request, attribution, distance, surfaces |

## Supported Actions

```text
retrieve
access_paid_content
purchase_access
invite_create
invite_redeem
revoke_access
discover
reshare
request_introduction
external_write
notify
export
report
moderation_review
delete
view_audit_history
rank_eligibility
```

Each action is evaluated through action-scoped helper APIs: `evaluate_retrieve`, `evaluate_discover`, `evaluate_reshare`, `evaluate_introduction`, `evaluate_external_write`, `evaluate_paid_access`, plus equivalent helpers for remaining actions. A caller receives only the decision for its requested action.

## Inputs

| Input | Description |
|---|---|
| `action` | Enumerated requested action |
| `post_id`, `policy_id`, `policy_snapshot_id`, `publication_snapshot_id` | Canonical object IDs where applicable |
| `policy_schema_version`, `evaluator_semantics_version` | Compatibility/interpretation versions |
| actor/recipient identity; author identity | Pseudonymous internal IDs and role context |
| immediate audience state | Audience snapshot membership, invite state, revocation state |
| discovery bridge consent | Scope, context, eligibility, and anonymity rules; never path output |
| recipient_preference_constraints | Opt-outs for discovery/intros/topics/communities/promotional or paid content/reshare approval |
| community charter rules | Charter version, membership/role constraints, and non-overridable platform protections |
| blocks/mutes | Directional block and mute relationships |
| access_restrictions | Account/post restriction, suspension, incident containment, age/region, order-driven access limitation |
| safety_enforcement_state | Abuse controls, rate limits, discovery suppression, quarantine, review state |
| retention_restrictions | Legal hold, preservation, backup retention, deletion pause; does not automatically deny ordinary access |
| time state | Deterministic UTC clock and lifecycle state |
| destination type | Native private/Open, notification, export, API, adapter destination |
| adapter capability | Capability manifest, consent receipt, scope, health, compliance status |
| entitlement/transaction state | Purchase, subscription, gift, refund, chargeback, and revocation state |
| ranking context | Ordering preference only; cannot alter authorization |

Missing required input yields `DENY_INPUT_INVALID`; protected actions fail closed.

## Action-Scoped Result

```text
EvaluationResult
- action
- decision: allow | deny | allow_with_constraints
- explanation_code
- constraints[]
- policy_snapshot_id
- publication_snapshot_id
- evaluator_semantics_version
- audit_class
```

The result never returns unrelated capabilities. A discovery evaluation never returns retrieval, external-write, or paid-access eligibility.

## Precedence

All actions begin with universal denials. Lower layers never override a higher denial.

1. **Access restrictions and safety enforcement:** blocks, deletion/revocation, suspension, active containment, age/region/order-driven limitation, and safety restrictions.
2. **Action authorization and eligibility:** required actor role, author authority, recipient/account binding, private publication snapshot, invite validity, and action-specific eligibility.
3. **Community, bridge, and recipient preferences:** charter limitations, bridge-consent scope, anonymity threshold, and recipient preference constraints.
4. **Time policy:** schedules, expiry, review locks, gradual-release state, rate limits, and time windows.
5. **Distribution and destination:** enabled channel, reshare constraints, destination rule, consent receipt, adapter capability.
6. **Entitlement or transaction state:** only for actions requiring it; purchase may be allowed before entitlement exists, while retrieval of paid content requires active entitlement.
7. **Ranking preference:** orders already eligible material only; never changes authorization.

`retention_restrictions` apply to retention/deletion processing, not ordinary user access unless a separately specified legal/safety order creates an access restriction.

## Action Rules

| Action | Minimum allow condition |
|---|---|
| `retrieve` | Subject is access-authorized by publication snapshot/Open policy and has active entitlement if paid |
| `access_paid_content` | Retrieval conditions plus active entitlement |
| `purchase_access` | Offer active; subject eligible to buy; destination/payment route valid; no restriction; successful transaction creates/updates entitlement |
| `invite_create` | Author authority, target/state validation, rate limit, and audience/policy conditions pass |
| `invite_redeem` | Token valid, recipient-bound verification succeeds, no revocation/restriction; redemption creates narrow trigger-post/future-eligible authorization, never back-catalog access |
| `revoke_access` | Authorized author/system/deletion/block action; revokes tokens/sessions/future access per policy |
| `discover` | Discovery rule, bridge/community/recipient preferences, and safety/anonymity constraints pass; no private retrieval implied |
| `reshare` | Subject is eligible, reshare enabled, constraints/destination pass, and attribution/approval requirements are met |
| `request_introduction` | Context and reciprocal preferences allow request; no private post access implied |
| `external_write` | Content is native-public, destination allowed, durable consent receipt valid, adapter capability valid; private material never qualifies |
| `notify` | Recipient is authorized; preview is non-sensitive/minimized; otherwise suppress details |
| `export` | User-owned records only; excludes third-party private identifiers/contact data absent valid consent/legal basis |
| `report` | Reporter can create a minimum-evidence case; evidence expansion is limited to authorized review workflow |
| `moderation_review` | Separately audited, role/purpose-limited case access only |
| `delete` | Applies revocation/live-content deletion while retention restrictions govern preservation/backups/legal holds |
| `view_audit_history` | Bounded, role-appropriate policy/distribution history with no protected topology or third-party private data |
| `rank_eligibility` | Subject is already eligible through another action evaluation |

## Blocks and Mutes

A block prevents new direct interaction, invitations, discovery bridging, and recommendation between blocker and blocked account. It also revokes private access where product policy specifies that a block revokes audience membership.

A block does not automatically erase unrelated Open content otherwise publicly available, unless a stronger block model is explicitly selected. A mute affects ranking/notification preferences, not authorization.

## Constraints

Constraints are action-specific, non-topological, safe to expose, and versioned in the schema registry.

```text
CONSTRAINT_COARSENED_EXPLANATION
CONSTRAINT_NO_RESHARE
CONSTRAINT_ATTRIBUTION_REQUIRED
CONSTRAINT_APPROVAL_REQUIRED
CONSTRAINT_RATE_LIMITED
CONSTRAINT_COMMUNITY_ONLY
CONSTRAINT_NO_EXTERNAL_EXPORT
CONSTRAINT_ENTITLEMENT_REQUIRED
CONSTRAINT_NOTIFICATIONS_SUPPRESSED
CONSTRAINT_PURCHASE_AVAILABLE
```

## Explanation Codes

| Code | Safe meaning |
|---|---|
| `ALLOW_ACTIVE_AUDIENCE` | You are in the current authorized audience |
| `ALLOW_OPEN_POLICY` | Available under its Open policy |
| `ALLOW_COMMUNITY_CONTEXT` | Available through selected community context |
| `ALLOW_BRIDGE_CONTEXT` | Available through opted-in shared context; path not disclosed |
| `ALLOW_ENTITLEMENT_ACTIVE` | Your paid-access entitlement is active |
| `ALLOW_PURCHASE_AVAILABLE` | This offer is available for purchase |
| `ALLOW_EXTERNAL_WRITE_CONSENTED` | External destination is approved and acknowledged |
| `DENY_BLOCKED` | This action is unavailable |
| `DENY_DELETED_OR_REVOKED` | Content or access is no longer available |
| `DENY_PRIVATE_SNAPSHOT` | You are not in the authorized audience |
| `DENY_DISCOVERY_UNAVAILABLE` | This opportunity is unavailable through current settings and context |
| `DENY_COMMUNITY_RULE` | Community rules do not permit this action |
| `DENY_TIME_POLICY` | Content is unavailable at this time |
| `DENY_DESTINATION_POLICY` | Destination is not permitted |
| `DENY_ADAPTER_CAPABILITY` | Connected destination cannot perform this action |
| `DENY_ENTITLEMENT` | Paid access is not active |
| `DENY_SAFETY_RESTRICTION` | Action is restricted for safety or legal reasons |
| `DENY_INPUT_INVALID` | Action cannot be completed safely |

Internal reason codes may distinguish `ANONYMITY_THRESHOLD_NOT_MET`; that detail never appears in user-facing explanation output.

## Idempotency, Caching, and Versioning

- State-changing actions require an idempotency key and produce an auditable receipt.
- Protected decisions cache only within a bounded TTL and must revalidate block, revocation, audience snapshot, entitlement, and restriction state before allow.
- Evaluator cache failure, stale revocation, stale block state, or schema/semantic incompatibility fails closed for protected actions.
- Each evaluation returns `policy_snapshot_id`, `publication_snapshot_id`, and `evaluator_semantics_version` for historical explainability.
- Policy schema changes and evaluator semantic changes are independently versioned. Semantic changes require a decision-register entry, migration plan, rollback plan, and compatibility tests.
- Historical posts remain interpretable under their publication snapshot and evaluator semantic version unless an approved migration changes future behavior.

## Test Cases

| ID | Scenario | Expected result |
|---|---|---|
| PEC-001 | Active recipient retrieves private post | Allow `ALLOW_ACTIVE_AUDIENCE` |
| PEC-002 | Follow-only user retrieves private post | Deny `DENY_PRIVATE_SNAPSHOT` |
| PEC-003 | User added after publication retrieves historical private post | Deny unless narrow trigger-post exception |
| PEC-004 | Valid invite redeemed | Trigger/future eligible access only; no back catalog |
| PEC-005 | Removed/blocked recipient uses token/session | Deny; revoke future access |
| PEC-006 | Discovery lacks bridge consent | Deny without topology disclosure |
| PEC-007 | Consent exists but anonymity threshold fails | `DENY_DISCOVERY_UNAVAILABLE`; no count/path leak |
| PEC-008 | Community policy conflicts with author preference | More restrictive valid rule wins |
| PEC-009 | Gradual release before window | Deny `DENY_TIME_POLICY` |
| PEC-010 | Recipient attempts disallowed reshare | Deny destination/distribution policy |
| PEC-011 | Private post enters adapter queue | Deny; no egress payload |
| PEC-012 | Public post cross-posts with valid consent/capability | Allow external write |
| PEC-013 | External write lacks receipt or scope | Deny |
| PEC-014 | Paid content has active entitlement | Retrieval allowed after earlier checks |
| PEC-015 | Refund/chargeback revokes access | Deny entitlement |
| PEC-016 | Ranking requests unauthorized private post | Deny; ranking cannot authorize |
| PEC-017 | Preview/enforcement semantic mismatch | Alert, fail closed for protected action |
| PEC-018 | Mute relationship | Does not deny authorization; may suppress ranking |
| PEC-019 | Block relationship | Applies directional block rules consistently |
| PEC-020 | Safety access restriction after publication | Restrict and audit reason |
| PEC-021 | Forwarded invite token opened by mismatched account | Deny; no audience change; security event |
| PEC-022 | Invitee reports before signup | Minimum-evidence report allowed; no content expansion |
| PEC-023 | Private-post notification generated | Only authorized recipient receives minimized preview |
| PEC-024 | Recipient opts out of bridge discovery | Deny without source/path disclosure |
| PEC-025 | Sparse graph creates apparent bridge route | Discovery unavailable/coarsened; no leakage |
| PEC-026 | Author changes community context after publish | Historical snapshot behavior remains defined; no silent expansion |
| PEC-027 | Export includes relationship records | Own records only; third-party private IDs/contact data excluded |
| PEC-028 | Post under legal hold is deleted | Access revocation follows policy; preservation follows hold process |
| PEC-029 | Purchase attempted before entitlement | Purchase may allow; retrieval denied until confirmation |
| PEC-030 | Adapter token revoked while queued | Cancel/retry only after renewed consent; native post intact |
| PEC-031 | Evaluator cache has stale block/revocation | Revalidate or fail closed |
| PEC-032 | Explanation would reveal bridge/community state | Return generic non-topological code |

## Assurance Requirements

- Unit and property tests prove lower layers cannot override higher denials.
- Integration tests cover compose, publication, retrieval, feed, invites, discovery, notifications, adapters, commerce, reports, deletion, export, and staff-review paths.
- Golden tests compare preview output with enforcement outcome for the same snapshot/semantic version.
- Fuzz malformed policy objects, version incompatibilities, stale state, and adapter receipts.
- Red-team topology inference, invitation forwarding, notification preview, private egress, and privileged access.
- No evaluator release proceeds without passing contract suite, traceability update, and security review.

## Audit and Observability

Protected decisions emit restricted audit records containing action, decision, safe explanation code, policy/publication snapshot IDs, evaluator semantics version, pseudonymous actor IDs, and timestamp. Consent receipts are append-only. Product analytics receives only approved minimum metadata. Evaluator mismatch, attempted fail-open, stale protected-state cache, and private egress alert security on-call.