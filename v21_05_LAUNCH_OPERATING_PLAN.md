# Launch Operating Plan

**Project:** Social Distance as Interface  
**Version:** v21  
**Owner:** Founder / Build Lead / Community Operations Lead  
**Readers:** Founder, build lead, operators, moderators, advisors  
**Controls:** Launch cohort, sequencing, staffing, metrics, gates, cut order, rollback decisions  
**Depends on:** `00_PRODUCT_CONSTITUTION.md`, `02_PRODUCT_PRD.md`, `03_TRUST_SECURITY_SAFETY.md`, `04_COMMERCE_OWNERSHIP.md`

## Launch Thesis

Launch is not “a complete social network.” It is a controlled proof that users can understand and repeatedly use honest private-audience posting, pairwise activation, and bounded consented introductions without surprise or unacceptable safety cost.

## Launch Community Criteria

Select 2-3 communities of about 150-250 potential members each. Each must have:

- Shared purpose and real interaction demand
- Existing trust norms and identifiable membership boundaries
- Willing operators with time and legitimacy
- Sufficient density and member overlap for introductions
- Clear exclusion/safety considerations
- A reason to use private posts and opportunity discovery
- Willingness to sign a charter and use reporting/appeal processes

Communities are validation cohorts, not a bespoke managed-service model. A replication playbook is required before expansion.

## Graph Bootstrap Priority

1. Pairwise invite through private posts or direct invitation
2. Operator-approved community entry
3. Contact import with local matching where feasible, explicit confirmation, and minimal retention
4. External account linking that imports provenance-labeled candidate edges
5. Interest/project participation through Looking For cards and project rooms
6. Search and broader public discovery after density and safety gates

Imported candidates show provenance: source, confirmation status, last refresh, removal option, and conversion path to native relationship. They never independently authorize private access, bridge consent, reputation, governance, or economics.

## Operator Program

### Operator responsibilities

- Communicate community charter and onboarding norms
- Moderate within charter scope
- Support initial member activation
- Curate community context and safe introduction practices where authorized
- Escalate safety incidents according to SLA

### Operator boundaries

Operators cannot view private posts, private-audience lists, or private interactions by default. Their permissions are explicit, minimum necessary, logged, reviewable, and replaceable.

### Required operator assets

- Charter template
- Training and safety playbook
- Escalation contact
- Moderation and appeal workflow
- Replacement/removal process
- Community health dashboard
- Replication checklist

## Phases

### Phase 0: Days 1-14 — Commitments and Readiness

- Freeze constitution, protected vocabulary, and product invariants
- Finalize legal/finance decision plan, runway/capital branch, and selected corporate direction
- Complete privacy, retention, moderation, identity, payment, and adapter compliance review plans
- Define every metric with formula, denominator, threshold, owner, cadence, and response
- Select/prepare launch communities; begin outreach Day 1
- Complete charter, operator training, incident, and replication materials
- Establish code ownership, security review, and release process

### Phase 1: Days 15-60 — Core Trust Loop

- Native identity/follows and optional adapter-link foundation
- Private posts, audiences/presets, truthful compose counts, token invite flow, revocation, snapshots
- Following feed, basic policy controls, bridge-consent settings, native Open posting
- Safety baseline, export/deletion/session/recovery, audit logs, and instrumentation
- Run operator onboarding and closed usability/safety testing

### Phase 2: Days 61-100 — Bounded Introduction Proof

- Launch 2-3 invite-gated communities
- Launch Looking For cards, request-introduction, and project-room experiments
- Validate audience comprehension, activation, retention, safety, and meaningful-connection metrics
- Publish initial value-flow ledger; add MVP tips/PWYW only if Tier 1 quality is stable
- Ship targeted-harassment and brigade controls before expansion

### Phase 3: Days 101-120 — Controlled Expansion

- Expand only through cohorts supported by the replication playbook
- Keep discovery bounded unless gates pass
- Treat adapter launches and broad commerce expansion as optional, not launch requirements
- Conduct launch review: continue, pause, narrow, or stop based on predefined evidence

## Capacity and Cut Order

### Tier 1: Cannot Slip

- Native identity/graph boundaries
- Private authorization, snapshots, invite tokens, revocation, deletion
- Compose truthfulness and no-topology-leak controls
- Native public writes and external-write consent boundary
- Testable security invariants, export, session/recovery, audit logs
- Block/report/rate-limit/invite-abuse controls

### Tier 2: Differentiated, Heavy Review

- Bounded introductions and bridge consent
- User-controlled ranking/explanations
- Community charter/operator tooling
- Value-flow ledger and narrow MVP commerce

### Tier 3: Cut in Order

1. Advanced search filters
2. Full moderation queue beyond functioning baseline
3. Secondary-flow WCAG AA (primary trust flows remain AA)
4. Reposts
5. Granular notification preferences
6. Advanced feed modes
7. Complex relationship-memory UI
8. Broad Open-network discovery
9. Native DMs
10. Expanded commerce suite
11. Adapter convenience features

**Day-30 pressure valve:** if Tier 1 velocity is at risk, invitation delivery launches copy/share-link only. Adapter-native DM convenience moves post-launch. Tier 1 does not slip.

## Metrics Dashboard

| Metric | Definition | Owner | Cadence | Gate / response |
|---|---|---|---|---|
| Private audience activation | Activated new users who create a private post or join a private audience within 7 days / activated new users | Product | Weekly | Floor set Phase 0; simplify onboarding if missed |
| Invite conversion | Unique invitees activated within 7 days / valid delivered invites | Growth | Weekly | Floor set Phase 0; revise channel/copy/verification |
| Audience comprehension | Test users correctly identify who can view and who may discover a test/last post / tested users | Research | Biweekly | Must meet launch threshold; block radius expansion if not |
| Meaningful connection rate | Active users with accepted intro, reciprocal follow, substantive reply, paid support, or project participation within 14 days / active users | Product | Weekly | Floor set Phase 0; revise bounded discovery |
| Safety veto rate | Serious privacy, invitation, or unwanted-discovery incidents / 1,000 active users | Safety | Weekly + immediate | Threshold breach freezes relevant expansion |
| Week-4 retained private users | New users active in private posting/viewing in week 4 / activated cohort | Product | Cohort | Indicates durable core-loop value |
| Creator transaction success | Successful paid-access/payout events / attempted payment events | Finance | Weekly | Controls commerce rollout |
| Community health | Active members, moderation load, unresolved reports, repeat participation | Ops | Weekly | Triggers operator support/pause |

Phase 0 must supply numeric thresholds, data source, event names, denominators, owners, and explicit decision dates for every row.

## North Star and Safety Veto

**Outcome north star:** weekly active users with a verified meaningful interaction: second private post, accepted introduction, mutual follow, sustained reply exchange, paid support, or project-room participation.

**Safety veto:** serious unwanted-exposure incidents per 1,000 active users. Any breach blocks expansion of the relevant feature, regardless of engagement or growth.

**Comprehension gate:** percent of posters who correctly identify who could see their last post. The product does not expand reach modes when users cannot reliably understand them.

## Pause, Rollback, and Kill Criteria

| Condition | Action |
|---|---|
| Confirmed private-content exposure | Immediate incident response; halt affected surface; assess notification; no expansion |
| Confirmed topology/intermediary leak | Disable affected discovery path; red-team remediation required |
| Invite abuse exceeds threshold | Tighten limits/verification; pause invite growth experiments |
| Community operator failure | Pause community expansion; replace/support operator; review charter |
| Tier 1 milestone miss | Trigger cut order; no scope substitution with Tier 2/3 work |
| Comprehension below threshold | Simplify compose/presets; keep advanced reach hidden |
| No sustained private-loop retention after defined test | Narrow wedge or stop broader-platform investment |
| Discovery shows harm without relationship formation | Retain private utility; suspend discovery work |

## Runway and Staffing

The founder states runway and capital plan in Phase 0. Build and safety commitments are planned against that reality; the document does not assume unbounded runway.

Minimum accountable roles: founder/product owner, human build lead for Tier 1, security/trust reviewer, community/operator lead, and defined moderation coverage. Agentic capacity may accelerate implementation but cannot replace human accountability for Tier 1, safety, or legal decisions.

## Changelog

- **v21:** Extracted from v20; adds bootstrap lifecycle, metric definitions, paired north-star/safety-veto design, and explicit pause/rollback/kill rules.