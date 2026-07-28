# Open Questions Register

**Project:** Social Distance as Interface  
**Phase:** 0 hardening pass v2  
**Authority:** Scope-control register; not a source of public commitments  
**Owner:** Founder  
**Review:** Twice weekly in Phase 0; blocker review on Day 7 and Day 14

| ID | Question | Severity | Class | Owner | Needed by | Depends on | Default if unresolved | Decision meeting | Evidence |
|---|---|---|---|---|---|---|---|---|---|
| OQ-001 | First adapter capability | Non-blocking if deferred | Architecture | Founder + Eng + Sec | Before adapter implementation starts | — | No adapter in v1; no adapter code or OAuth scope enters the core launch path | Day 7: defer/choose only | Onboarding/compliance estimate |
| OQ-002 | Corporate/mission-lock structure | Public-economic-claim blocker | Legal | Founder + Counsel | Phase 0 close | Runway/financing | No ownership/surplus claim beyond fees/ledger; do not market community-owned, participant-owned, shared-upside, profit-sharing, surplus, or governed-fund claims unless legally and operationally defined | Day 14 | Legal/tax/securities analysis |
| OQ-003 | Fee schedule/cap/reserve/payout terms | Paid-commerce blocker | Finance/legal | Founder + Finance + Counsel | Before paid claim | OQ-011 | Disable paid access/payouts | Day 14 | Unit economics/processor terms |
| OQ-004 | E2EE roadmap | E2EE-claim blocker | Security | Security + Founder | Before expanded privacy claim | Recovery model | State server-private, not E2EE | Day 14 | Threat/recovery design |
| OQ-005 | Invite identity/recovery assurance | Invite-beta blocker | Security | Security + Product | Before invite beta | Identity policy | Do not enable external invite redemption | Day 10 | Abuse/usability tests |
| OQ-006 | Numeric Launch Scorecard thresholds | Cohort-launch blocker | Product/ops | Product + Research + Safety | Day 10-14 | Event readiness | Do not expand beyond usability cohort | Day 10 | Baselines/sample plan |
| OQ-007 | Minimum community density profile | Cohort-launch blocker | Operations | Ops + Product | Before selection | OQ-006 | Do not select cohort | Day 10 | Community interviews/model |
| OQ-008 | Operator classification/compensation | Cohort-launch blocker | Ops/legal | Ops + Finance + Counsel | Before launch | OQ-002 | No unsupported moderation role | Day 14 | Workload/funding/legal review |
| OQ-009 | Private-report evidence scope | Beta blocker | Safety/legal | Safety + Legal + Security | Before reporting | Incident process | Restrict to reported item only | Day 10 | Harm/appeal review |
| OQ-010 | Crowd thresholds for bridge/reach estimates | Bridge-beta blocker | Product/security | Product + Security + Safety | Before bridge beta | Graph tests | Disable bridge discovery/proximity estimates | Day 14 | Inference/red-team tests |
| OQ-011 | Payment liability/refund/chargeback model | Paid-commerce blocker | Finance/legal | Finance + Counsel | Before paid MVP | OQ-002, OQ-020 | Disable payments/payouts | Day 14 | Processor/tax analysis |
| OQ-012 | Non-overridable community charter defaults | Cohort-launch blocker | Policy | Product + Safety + Legal | Before charter | DEC-024 | Use strict platform default | Day 10 | Operator/abuse review |
| OQ-013 | Retention windows by data class | Beta blocker | Security/legal | Security + Legal | Before beta | Data inventory | Minimize collection; no undeclared retention | Day 14 | Legal/privacy/cost analysis |
| OQ-014 | Accessibility/localization launch scope | Beta blocker for affected flows | Product/design | Product + Design | Before beta | User research | Core trust flows WCAG AA | Day 14 | Accessibility review |
| OQ-015 | Canonical identifier/handle/rename/merge policy | Identity-beta blocker | Product/security | Product + Security | Before identity beta | OQ-005 | Immutable internal ID; conservative public rename | Day 10 | Impersonation/account model |
| OQ-016 | First contact-import consent/local match/deletion flow | Contact-import blocker | Privacy/product | Product + Security | Before import decision | OQ-001, OQ-013 | No contact import | Day 10 | Consent/privacy design |
| OQ-017 | User-visible behavior when gradual release changes reach | Gradual-release blocker | Product | Product + Design + Security | Before feature | DEC-011 | Do not ship gradual release | Day 14 | UX/threat review |
| OQ-018 | Default mode/preset policy mappings | Compose-usability blocker | Product/design | Product + Design | Before usability test | DEC-019/020 | Three basic defaults only | Day 7 | Usability research |
| OQ-019 | Minor/age-gated content/community policy | General-access blocker | Legal/safety | Founder + Legal + Safety | Before general access | Jurisdiction scope | Adults-only closed cohorts | Day 14 | Legal/safety analysis |
| OQ-020 | MVP jurisdictions and payment availability | Paid-commerce blocker | Legal/finance | Counsel + Finance | Before paid commerce | OQ-002/011 | Restrict to approved jurisdiction/no payments | Day 14 | Jurisdiction analysis |
| OQ-021 | Creator transaction abuse model | Paid-commerce blocker | Finance/safety | Finance + Safety + Eng | Before PWYW/tips | OQ-011 | Disable paid commerce | Day 14 | Fraud scenarios/tests |
| OQ-022 | Definition of operator heroics | Expansion blocker | Operations | Ops + Founder | Before cohort measurement | OQ-006/008 | No replication claim | Day 14 | Time/support logs |