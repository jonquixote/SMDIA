# Launch Operating Plan

**Project:** Social Distance as Interface  
**Version:** v22  
**Owner:** Founder / Build Lead / Community Operations Lead  
**Readers:** Founder, build lead, operators, moderators, advisors  
**Authority level:** Operating plan  
**Changes require:** Relevant operating owner; higher-level review if a change affects constitutional/binding rule  
**Review cadence:** Weekly during launch, at each gate, after SEV-0/SEV-1  
**Conflicts resolved by:** `00_PRODUCT_CONSTITUTION.md`  
**Last cross-document consistency review:** 2026-07-27

## Launch Thesis

Launch proves a narrow trust-and-connection loop: users understand and repeatedly use private-audience posting, honest activation, and bounded consented introductions without unacceptable safety cost. Feature parity is not a launch objective.

## Phase 0 Mandatory Deliverable: Launch Scorecard v1

**Locked by Day 14.** No expansion decision may use undefined metrics.

| Metric | Formula / event names | Initial threshold | Owner | Locked by | Gate / miss response |
|---|---|---:|---|---|---|
| Private-audience activation | `private_post_published` or joined audience within 7 days / activated users | TBD | Product | Day 10 | Onboarding revision |
| Audience comprehension | Correctly identify current viewers and discovery eligibility / tested users | TBD | Research | Day 10 | Radius expansion blocked |
| Invite nuisance | Invitee `invite_blocked` or `invite_reported` / delivered valid invites | TBD | Safety | Day 10 | Tighten limits/verification |
| Serious private exposure | Confirmed incident count | 0 hard-stop | Security | Day 10 | Immediate expansion halt |
| Topology/unwanted discovery | Confirmed incidents / 1,000 WAU | TBD | Safety | Day 10 | Pause discovery surface |
| Account takeover/unsafe recovery | Confirmed incidents / 1,000 WAU | TBD | Security | Day 10 | Pause risky access flow |
| Meaningful connection | Defined qualifying interaction / WAU | TBD | Product | Day 14 | Continue/revise discovery |
| Week-4 private retention | Cohort active in private view/post during week 4 / activated cohort | TBD | Product | Day 14 | Wedge review |
| Report-SLA compliance | Reports within target SLA / eligible reports | TBD | Safety | Day 14 | Staffing/coverage change |
| Creator transaction success | Completed non-refunded payment/payout events / attempted events | TBD | Finance | Day 14 | Commerce gate |

The scorecard records minimum sample size, exclusions, data source, review cadence, decision authority, and required response to each miss.

## Community Selection and Density

Each of 2-3 launch communities (about 150-250 potential members) must meet defined thresholds for:

- Expected activated members within 30 days
- Members who already know at least two other members
- Likely private-audience relationships per activated user
- Operator coverage hours per week
- Existing cadence of meetings, projects, events, or conversations
- Expected legitimate introductions/Looking For usage
- Shared purpose, norms, safety fit, and willingness to operate under charter

## Operator Economics and Capacity

Before cohort launch, each operator role is classified: volunteer, employee, contractor, member steward, or compensated community role. The plan specifies payment/stipend/revenue-share eligibility, conflict disclosure, maximum workload, minimum moderation coverage, escalation SLA, replacement process, and what happens when a community cannot sustain safe moderation.

Operators cannot access private posts/audience lists by default. Community operators are not a substitute for platform safety coverage.

## Graph Bootstrap Order

1. Pairwise private-post/direct invite
2. Operator-approved community entry
3. Contact import with local matching where feasible, explicit confirmation, and minimal retention
4. External linking/import of provenance-labeled candidates
5. Looking For cards/project rooms
6. Search/broader discovery only after gates pass

## Phases

### Phase 0: Days 1-14

Freeze doctrine; complete legal/finance/security/adapters review plan; lock Scorecard v1; select/train operators; prepare charters, incident flows, and replication checklist; state runway/capital plan.

### Phase 1: Days 15-60

Build Tier 1 native core: identity/follows, private posts/audiences/invites/snapshots, feed policy, bridge settings, native Open post, export/deletion/session/recovery/audit/instrumentation; run closed testing.

### Phase 2: Days 61-100

Launch bounded cohorts, introductions/Looking For/project rooms; validate trust/comprehension/safety/retention; publish initial ledger; add narrow commerce only if Tier 1 is stable; ship anti-brigade controls before expansion.

### Phase 3: Days 101-120

Controlled invite-gated expansion only through repeatable cohorts. Adapter and broad-commerce work remain optional.

## Replication Gate: Do Not Scale

No community expansion until **at least two cohorts independently** meet private-loop retention, audience-comprehension, safety-veto, and meaningful-connection thresholds for **two consecutive measurement windows**, without founder/operator intervention beyond the documented baseline checklist.

## Safety Gates

- **Hard stop:** confirmed unintended private-content exposure; immediately halt relevant surface independent of rates.
- **Hard stop:** confirmed topology/intermediary leak; disable affected discovery path.
- **Trend gate:** invite abuse/harassment rate; tighten limits and pause growth experiments on breach.
- **Operational gate:** account takeover/unsafe recovery; pause affected auth/recovery path.
- **SLA gate:** report-response compliance; increase coverage or pause cohort expansion.

## Capacity and Cut Order

### Tier 1: cannot slip

Native relationship boundaries; private authorization/snapshots/tokens/revocation/deletion; policy evaluator/no-topology controls; external-write boundary; trust tests/export/session/recovery/audit; block/report/rate limits.

### Tier 2: differentiated

Bounded introductions; ranking explainability; operator/community tooling; initial value-flow ledger/narrow commerce.

### Tier 3 cut order

1. Advanced search
2. Full moderation queue beyond functional baseline
3. Secondary-flow WCAG AA (primary trust flows remain AA)
4. Reposts
5. Fine-grained notifications
6. Advanced feed modes
7. Complex relationship-memory UI
8. Broad discovery
9. Native DMs
10. Expanded commerce
11. Adapter convenience features

If Tier 1 is overloaded on Day 30, launch invitation delivery with copy/share links only; defer adapter-native delivery.

## Changelog

- **v22:** Adds Day-14 Scorecard contract, disaggregated safety gates, measurable density criteria, operator economics, and a two-cohort/no-heroics replication rule.