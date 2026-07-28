# Trust, Security, and Safety Specification

**Project:** Social Distance as Interface  
**Version:** v22  
**Owner:** Security / Build Lead  
**Readers:** Engineering, security, operations, legal, moderation  
**Authority level:** Binding specification  
**Changes require:** Security + engineering approval; legal review for retention/legal-process changes  
**Review cadence:** Monthly, before launch gate, after SEV-0/SEV-1, and after material adapter change  
**Conflicts resolved by:** `00_PRODUCT_CONSTITUTION.md`  
**Last cross-document consistency review:** 2026-07-27

## Security Contract

Private content is server-private and encrypted at rest, not end-to-end encrypted at MVP. Security controls must make the constitutional promises mechanically true, particularly `CONST-TRUST-001` through `003`, `CONST-BRIDGE-001`, and `CONST-GRAPH-003`.

## Data and Encryption Posture

| Asset/store | Encryption and access posture |
|---|---|
| Primary databases | Encryption at rest; application roles least-privilege; production access controlled and audited |
| Object/attachment storage | Separate encryption domain; short-lived signed URLs; recipient authorization before URL issuance |
| Backups | Encrypted separately; retention/deletion/restore access documented |
| Queues/caches | No private plaintext unless necessary; TTL, encryption, and authorization documented |
| Search indexes | Private content excluded unless an authorized private-search design is approved; indexes enforce same authorization |
| Logs/analytics | No private plaintext; minimize derived private metadata; restricted retention |
| Keys | Managed KMS/HSM-equivalent; rotation policy; access separated from ordinary application access; key-use audit trail |

The exact vendor may change; this posture may not weaken without a constitutional amendment or documented security emergency.

## Permission Matrix

| Role | May access private content? | Basis | Audit requirement |
|---|---|---|---|
| Community operator | No by default | Never for ordinary moderation | Attempts logged |
| Automated safety system | Only narrow, documented signals/content if enabled | Approved rule/model | Decision trace + retention rule |
| Report reviewer | Only report-scoped evidence | User report/escalation | Time-bound audited access |
| Security responder | Only incident-scoped | SEV incident | Dual authorization where feasible; audited |
| Support staff | No by default | Exceptional case-bound escalation | Audited case record |
| System administrator | No content access by default | Infrastructure maintenance | Access separation and logs |

## Threat Model Matrix

| Threat | Asset at risk | Likely actor | Entry point | Control | Detection | Owner |
|---|---|---|---|---|---|---|
| Invite forwarding | Private post access | Recipient/attacker | Invite token | Recipient binding, verification, rate limits | Redemption anomalies | Security |
| Topology inference | Relationship privacy | Curious/malicious user | Search/reach estimates | Crowd thresholds, coarsening, no enumeration | Red-team probes | Product + Security |
| Insider access | Private content | Staff/contractor | Admin tools | Least privilege, JIT access, audit logs | Log review | Security |
| Adapter compromise | External-write integrity | Token thief/platform issue | OAuth/export queue | Scope isolation, revocation, allowlists | Egress/token alerts | Engineering |
| Brigade harassment | User safety | Coordinated accounts | Replies/invites/public posts | Rate limits, detection, escalation | Incident dashboard | Safety |
| Account takeover | Identity/private content | Attacker | Session/recovery | MFA-capable design, session controls, recovery challenge | Risk alerts | Security |
| Report abuse | Private context | Malicious reporter | Report workflow | Report-scoped evidence, reviewer limits | Sampling/audit | Safety |

## Abuse-Report Privacy

- A report grants reviewers access only to the specific reported item by default.
- Related context is separately requested, user-provided, or rule-authorized; it is not silently opened wholesale.
- Authors receive notice only when it does not increase safety risk or compromise investigation.
- Appeal evidence is redacted to minimum necessary detail.
- Malicious submission of private content is itself reviewable abuse.
- Community operators do not receive private-post evidence unless a narrowly defined, user-visible charter process and security approval permits it.

## Risk Register

| Threat | Likelihood | Impact | Controls | Detection | Owner | Review | Residual-risk acceptance |
|---|---|---|---|---|---|---|---|
| Private egress | Low target | Critical | Egress isolation, tests | Alerts/tests | Security | Monthly | Founder + Security |
| Topology leak | Medium | High | Coarsening, thresholds | Red team | Product/Security | Monthly | Founder + Security |
| Invite abuse | Medium | Medium/High | Verification/rate limits | Reports/anomalies | Safety | Weekly | Safety lead |
| Operator abuse | Low/Medium | High | Permission limits/audit | Audits/reports | Ops/Safety | Monthly | Founder |
| Adapter scope drift | Medium | Medium | Manifest/review | Token/API audit | Engineering | Per release | Security |

## Invariants and Tests

| Rule | Verification |
|---|---|
| CONST-TRUST-001 | Compose count derived only from active recipients; contract and integration tests |
| CONST-TRUST-002 | Snapshot authorization tests reject later additions except valid trigger-token exception |
| CONST-TRUST-003 | Remove/block/delete/expiry invalidation tests |
| CONST-GRAPH-003 | Shared policy-evaluator tests; preview cannot overstate delivery |
| CONST-BRIDGE-001 | Graph-inference red team, response filtering, threshold tests |
| CONST-ECON-001 | Ledger/audit/version checks for fee and payout representation |

Test suite includes units, integration tests, property/fuzz tests for authorization/tokens, egress scanning, red-team topology inference, dependency/credential scans, privileged-access review, and tabletop exercises.

## Deletion, Retention, Legal Holds

Live data, backups, logs, legal holds, and external copies are distinct. Deletion removes live retrieval and revokes invitations; encrypted backup and DR deletion follows published windows; holds are scope-limited/logged; external copies follow destination policy and are disclosed. Export covers user-owned content/policy/eligible records under `CONST-PORT-001`.

## Incident Severity

| Severity | Example | Required response |
|---|---|---|
| SEV-0 | Broad confirmed private exposure | Halt affected surface; executive/security incident; notification assessment |
| SEV-1 | Single-user unauthorized private access/topology leak/account takeover | Contain, investigate, remediate, assess notification |
| SEV-2 | Invite abuse pattern/control bypass | Rate-limit/disable path; investigate/fix |
| SEV-3 | Confusing UX/non-sensitive defect | Triage, patch, monitor |

## Changelog

- **v22:** Adds encryption/key posture, permission matrix, threat matrix, report-privacy rules, and living risk register.