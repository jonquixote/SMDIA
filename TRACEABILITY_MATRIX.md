# Traceability Matrix

**Project:** Social Distance as Interface  
**Phase:** 0 hardening pass v2  
**Authority:** Release-readiness verification index  
**Owner:** Product + Security  
**Review:** Before release and launch gates

| Promise | Rule | Requirement/control | Metric/gate | Risk | Feature owner | Assurance owner | Gate | Test | Instrumentation | Release evidence | Engineering assurance | Product/operational validation |
|---|---|---|---|---|---|---|---|---|
| I know who can see this now | CONST-TRUST-001 | Shared evaluator; active vs invitee preview | Comprehension threshold | Critical | Contract + integration | Specified | Preview/delivery test suite | Requirement not decomposed |
| My audience does not silently expand | CONST-TRUST-002 | Snapshot authorization | Exposure hard stop | Critical | Snapshot integration | Specified | Access regression suite | Requirement not decomposed |
| Removal stops future access | CONST-TRUST-003 | Revoke tokens/sessions/authorization | Revocation failures | Critical | Revocation integration | Specified | Access audit | Requirement not decomposed |
| Opportunity reveals only what I understand | CONST-BRIDGE-001 | Mode preview; bridge consent; coarsened labels | Discovery incidents | High | UX + policy tests | Specified | Research + red team | Requirement not decomposed |
| I can disable network discoverability | CONST-BRIDGE-001 | Scope-specific bridge opt-out | Opt-out effectiveness | High | Policy tests | Specified | Settings test suite | Requirement not decomposed |
| Hidden paths are not revealed | CONST-BRIDGE-001 | Thresholds/response filters | Topology hard stop | Critical | Red-team inference | Specified | Red-team report | Requirement not decomposed |
| Public cross-post cannot export private material | CONST-TRUST-001 | Public-only typed export queue | Private-egress hard stop | Critical | Egress integration | Specified | Queue/egress tests | Requirement not decomposed |
| I can change feed behavior | CONST-METRIC-001 | Explainable editable feed policy | Policy use/complaints | Medium | UX tests | Specified | Feed-policy test | Requirement not decomposed |
| I can use product without another network | Canonical rule | Native activation/core loop | Adapter independence | High | Failure test | Specified | Adapter-off test | Requirement not decomposed |
| Operators cannot see private posts | CONST-TRUST-001 | Role restrictions/audit | Privileged violation hard stop | Critical | RBAC tests | Security audit stream | Permission matrix evidence | Requirement not decomposed |
| Deleted account revokes invites/follows per policy | CONST-TRUST-003 | Deletion/revocation/retention workflow | Deletion completion | High | Lifecycle tests | Specified | Deletion job audit | Requirement not decomposed |
| I can leave with work and records | CONST-PORT-001 | Export/deletion contract | Export completion | High | Export tests | Specified | Export sample | Requirement not decomposed |
| Creator rights remain mine | CONST-ECON-002 | Rights policy/license terms | Rights dispute rate | High | Terms/product tests | Specified | Counsel approval | Requirement not decomposed |
| Fees and splits compute correctly | CONST-ECON-001 | Ledger/reconciliation | Ledger accuracy | Critical | Financial unit/integration | Finance stream | Reconciliation report | Requirement not decomposed |
| Growth does not trade trust for engagement | CONST-METRIC-001 | Quality/safety companion metrics | Hard stops + trend gates | Critical | Metric governance review | Dashboard specified | Scorecard review | Requirement not decomposed |


| An invite link cannot silently authorize the wrong account | CONST-TRUST-001 | Recipient-bound token validation | Invite-beta hard stop | Critical | Product | Security | Invite-beta blocker | Contract + integration | Specified | Link/token validation suite | Requirement not decomposed | Not planned |
| An imported contact/follow does not become trust or permission | DEC-021 | Imported edges remain non-authoritative until converted by user action | Beta blocker | High | Product | Security | Beta blocker | Integration + UX | Specified | Import conversion audit | Requirement not decomposed | Research scheduled |
| Community rules cannot weaken platform safety guarantees | DEC-024 | Platform safety precedence over charters | Cohort-launch blocker | Critical | Product | Safety | Cohort-launch blocker | Policy tests | Specified | Charter override tests | Requirement not decomposed | Not planned |
| Reach estimates do not expose a sparse graph | CONST-BRIDGE-001 | Coarsened estimates only; no hidden path disclosure | Bridge-beta blocker | Critical | Product | Security | Bridge-beta blocker | Red-team + UX | Specified | Inference test suite | Requirement not decomposed | Not planned |
| External deletion behavior is explained before a native cross-post is published | DEC-021 | Destination-specific deletion disclosure | Adapter-beta blocker | High | Product | Security | Adapter-beta blocker | UX + integration | Specified | Disclosure test | Requirement not decomposed | Not planned |
| Payouts go to the right people and collaborator splits are deterministic | DEC-012/013 | Ledger/payout allocation correctness | Paid-beta blocker | Critical | Finance | Security/Finance | Paid-beta blocker | Reconciliation tests | Specified | Ledger evidence | Requirement not decomposed | Not planned |
| Private analytics do not contain private content or topology | DEC-022 | Metadata-minimized analytics only | Beta blocker | Critical | Product | Security | Beta blocker | Data review | Specified | Schema audit | Requirement not decomposed | Not planned |
| The user can understand and change a gradual-release policy before it begins | DEC-011 | Preview and edit gradual release | Gradual-release blocker | High | Product | Design/Security | Gradual-release blocker | Usability tests | Specified | UX evidence | Requirement not decomposed | Research scheduled |

## Status Values

- **Requirement not decomposed**
- **Test plan designed**
- **Test implemented**
- **Test passing in CI**
- **Validated in cohort**

Each row must record last verified date/release before a corresponding feature is enabled.