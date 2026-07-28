# Decisions Register

**Project:** Social Distance as Interface  
**Phase:** 0 hardening pass v2  
**Authority:** Binding decision record  
**Owner:** Founder  
**Change control:** New/reversed decisions require rationale, evidence, version/date, linked-document update, and migration note

| ID | Binding decision | Type | Effective | Decision status | Implementation | Verification | Release gate | Owner | Depends on | Supersedes | Migration | Review by | Evidence |
|---|---|---|---|---|---|---|---|---|---|
| DEC-001 | Only native canonical records may determine authorization, discovery eligibility, entitlements, governance, or policy enforcement | Structural | v1 launch | Approved | Not started | Pending | Beta blocker | Founder | — | — | No | Quarterly | Constitution/adapters review |
| DEC-002 | A follow cannot grant private-audience authorization | Constitutional | v1 launch | Approved | Not started | Pending | Beta blocker | Product | DEC-001 | — | Schema/UI | Before beta | CONST-GRAPH-002 |
| DEC-003 | Graph distance alone cannot grant retrieval, discovery, distribution, reshare, or external-write eligibility | Constitutional | v1 launch | Approved | Not started | Pending evaluator and red-team tests | Beta blocker | Product + Security | DEC-010; OQ-010 | — | Evaluator | Before beta | CONST-GRAPH-003 |
| DEC-004 | Bridge consent is opt-in and scope-specific | Constitutional | v1 launch | Approved | Not started | Pending | Bridge-beta blocker | Product + Safety | OQ-010 | — | Schema/UI | Before bridge beta | CONST-BRIDGE-001 |
| DEC-005 | Private posts use publication snapshots | Structural | v1 launch | Approved | Not started | Pending | Beta blocker | Eng + Security | DEC-010 | — | Schema | Before beta | Snapshot threat/test review |
| DEC-006 | Invitees must not be represented as current viewers before active authorization | MVP trust | v1 launch | Approved | Not started | Pending | Beta blocker | Product | DEC-005; DEC-010 | — | UI/events | Before beta | CONST-TRUST-001 |
| DEC-007 | Private posts are server-private, encrypted at rest, and not E2EE unless a later decision explicitly changes that posture | Time-bounded trust posture | v1 launch | Approved | Not started | Pending threat/recovery review | Public-claim blocker | Founder + Security | OQ-004; OQ-013 | — | Required if posture changes | Before public privacy-claim expansion | Threat/recovery review |
| DEC-008 | No private content, private metadata, private attachment reference, audience record, or topology data may enter an adapter write queue | Constitutional | v1 launch | Approved | Not started | Pending integration tests | Adapter-beta blocker | Security + Eng | DEC-001; adapter isolation design | — | Egress controls | Before adapter beta | Integration tests |
| DEC-009 | Compose begins with three calm defaults | MVP UX | v1 launch | Approved | Not started | Pending usability evidence | Usability gate | Product + Design | OQ-018 | — | UI | Usability gate | Research |
| DEC-010 | Policy preview and all access/discovery/distribution decisions must be computed from the same versioned `PostReachPolicy` evaluator | Structural | v1 launch | Approved | Not started | Pending contract/integration tests | Beta blocker | Product + Eng | POLICY_EVALUATOR_CONTRACT; OQ-010 | — | Required | Before beta | Contract tests |
| DEC-011 | Gradual release is a time/distribution modifier, not an audience level | Approved design; deferred implementation | When feature ships | Approved | Deferred | Not applicable until feature | Gradual-release beta blocker | Product | OQ-017; DEC-010 | — | Policy schema/UI | Before gradual-release beta | UX/threat review |
| DEC-012 | Tips, PWYW, named splits, ledger, and fund visibility may ship only after core-trust gates, processor/legal review, payout-liability design, and ledger reconciliation controls pass | Conditional MVP | After commerce gate | Approved | Not started | Pending finance/legal/controls | Paid-commerce blocker | Founder + Product | OQ-003; OQ-011; OQ-020; OQ-021 | — | Commerce schema | Before paid beta | Unit economics/legal |
| DEC-013 | Creator/customer payables are liabilities, not company surplus | Constitutional | Paid launch | Approved | Not started | Pending finance/counsel review | Paid-commerce blocker | Finance + Founder | DEC-012; OQ-011 | — | Ledger/accounting | Before paid beta | Finance/counsel |
| DEC-014 | Creator retains copyright; platform license is limited; no blanket AI training right | Constitutional | v1 launch | Approved | Not started | Pending counsel review | Launch terms blocker | Founder + Legal | OQ-020 | — | Terms/product | Before launch | Counsel review |
| DEC-015 | Adapters ship one capability at a time; sync is opt-in, visible, provenance-bearing, and non-authoritative | Structural | First adapter | Approved | Not started | Pending compliance review | Adapter-beta blocker | Founder + Eng | OQ-001; OQ-016 | — | Adapter lifecycle | Before adapter beta | Adapter spec |
| DEC-016 | Expansion requires two passing cohorts without founder/operator heroics | Operational | Cohort expansion | Approved | Not started | Pending cohort evidence | Expansion blocker | Founder + Ops | OQ-006; OQ-007; OQ-008; OQ-022; metrics taxonomy | — | Dashboard/playbook | Before cohort 1 | Launch plan |
| DEC-017 | Confirmed unintended private-content exposure is a hard stop | Safety | v1 launch | Approved | Not started | Pending runbook/audit tests | Beta blocker | Security + Safety | Incident definitions; runbook; audit logging | — | Incident runbook | Before beta | Glossary + taxonomy |
| DEC-018 | No core ranking, payout, discovery, or growth mechanism may optimize a single proxy—engagement, follows, invitations, time spent, or transactions—without explicit safety, quality, and anti-fraud constraints | Constitutional | v1 launch | Approved | Not started | Pending metric review | Launch blocker | Founder | Metrics taxonomy | — | Metric review | Quarterly | CONST-METRIC-001 |
| DEC-019 | Reach policy is multidimensional | Structural | v1 launch | Approved | Not started | Pending schema review | Beta blocker | Product + Eng | DEC-010 | — | Policy schema | Before beta | PRD/evaluator |
| DEC-020 | Named post modes are editable policy presets | Product | v1 launch | Approved | Not started | Pending usability testing | Usability gate | Product + Design | DEC-019; OQ-018 | — | UI | Usability gate | UX testing |
| DEC-021 | External sync is opt-in, user-visible, provenance-bearing, and non-authoritative | Structural | First adapter | Approved | Not started | Pending adapter tests | Adapter-beta blocker | Eng + Security | OQ-001; adapter compliance review | — | Adapter lifecycle | Before adapter beta | Adapter spec |
| DEC-022 | Private-content analytics are metadata-minimized: no plaintext, attachment URLs, raw invite tokens, or exact graph paths | Constitutional | v1 launch | Approved | Not started | Pending telemetry review | Beta blocker | Product + Security | OQ-013 | — | Telemetry pipeline | Before beta | Taxonomy/privacy review |
| DEC-023 | Advanced reach controls use progressive disclosure | MVP UX | v1 launch | Approved | Not started | Pending usability evidence | Usability gate | Product + Design | OQ-018 | — | UI | Usability gate | Research |
| DEC-024 | Community charter defaults cannot weaken platform safety guarantees | Constitutional | v1 launch | Approved | Not started | Pending charter review | Cohort-launch blocker | Founder + Safety | OQ-012; charter template; operator model | — | Charter templates | Before cohort launch | Constitution/charter review |

## Lifecycle

**Decision status:** Proposed -> Approved -> Superseded/Retired.  
**Implementation:** Not started -> In progress -> Implemented.  
**Verification:** Pending -> Test designed -> CI passing -> Operational/red-team/legal verified.  

A decision can be approved while implementation and verification remain incomplete. Emergency security/legal action may precede full documentation but requires retrospective record within five business days.