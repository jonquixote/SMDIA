# Glossary

**Project:** Social Distance as Interface  
**Phase:** 0 hardening pass v2  
**Authority:** Shared vocabulary; Constitution prevails on conflict  
**Owner:** Product Lead  
**Review:** Before launch gates and whenever a protected term or policy field changes

## `PostReachPolicy` Vocabulary

| Field | Definition |
|---|---|
| `immediate_audience_rule` | Who can retrieve the post at publication time |
| `discovery_rule` | Who may encounter the post later, if anyone |
| `distribution_rule` | Which channels are enabled at all: recommendation, reshare, introduction, external copy |
| `reshare_policy` | Constraints on person-to-person forwarding within an enabled reshare channel, such as request-before-reshare, attribution, distance, and permitted surface |
| `time_rule` | Expiry, review, schedule, or gradual-release behavior |
| `destination_rule` | Native public destinations and approved external destinations |
| `entitlement_rule` | Who may access: free, purchased, subscribed, gifted, or community-granted |
| `economic_rule` | Pricing, fees, payout allocation, splits, refunds, and payment terms |
| `rights_rule` | Licensing, remix, syndication, quoting, and AI-use permissions |
| `safety_constraints` | Rules that narrow or suppress otherwise eligible reach |
| `policy_schema_version` | Immutable policy schema/rule version used for preview and enforcement |

## Reach and Policy Terms

| Term | Definition | Must not imply |
|---|---|---|
| **Immediate audience** | People authorized to retrieve a post now | Later discovery eligibility |
| **Eligible reach** | Policy-qualified set of people who could encounter content later | Exact delivery or a guaranteed count |
| **Reach estimate** | Privacy-coarsened, non-guaranteed representation of eligible reach shown to author | A promise that those people will receive or see it |
| **Policy preview** | User-facing explanation computed from `PostReachPolicy` before publication | A different rule system than delivery |
| **Policy evaluator** | Versioned backend decision function for access, discovery, distribution, entitlement, and explanation | Ranking alone |
| **Distribution** | How content may move: recommendation, reshare, introduction, external copy | Authorization to retrieve private content |
| **Discovery eligibility** | Conditions for offering content or a relationship opportunity | Immediate access |
| **Gradual release / slow travel** | Time/distribution policy that starts small and expands only under author-selected consent/safety conditions | A peer audience level |
| **Audience preset** | Reusable named template proposing policy/audience settings, editable per post | Irrevocable access or a separate content type |
| **Community default** | Charter-defined policy template shown only when author deliberately selects a community context; it cannot override platform safety guarantees or silently alter audience, destination, or economic terms | A community override of platform safety guarantees |
| **Consent receipt** | Durable record of acknowledgment for external write, bridge consent, or material policy action | A blanket consent |

## Graph Terms

| Term | Definition | Must not imply |
|---|---|---|
| **Native follow** | Native edge meaning “I want to see this person” | Private access, bridge consent, endorsement, governance, or entitlement |
| **Private audience** | Explicit people authorized for a specific private post/preset | A follow list or permanent access |
| **Interaction graph** | Record of actual authorized engagement | Trust, intimacy, or entitlement |
| **Discovery bridge** | Consent-qualified path supporting contextual introduction/discovery | Endorsement, topology disclosure, or private access |
| **Bridge consent** | Opt-in, scope-specific permission for graph position to support a qualifying path | Permission to name intermediary or exact degree |
| **Economic graph** | Creation, funding, curation, stewardship, or allocation relationships | Social closeness or private influence |
| **Imported candidate edge** | External relationship data with provenance awaiting user action | Native follow, private audience, bridge, reputation, governance, or economic edge |
| **Stale imported edge** | Candidate data past declared source refresh window | Confirmed native relationship deletion |
| **Canonical record** | Native authoritative record for policy/authorization | An adapter reference/copy |
| **Topology leak** | Disclosure/inference of hidden paths, degrees, or intermediary identity | Authorized contextual discovery |

## Trust, Incident, and Access Terms

| Term | Definition |
|---|---|
| **Active recipient** | Person currently authorized by policy and publication snapshot to retrieve a post |
| **Invitee** | Person who may activate access with valid recipient-bound invite but cannot necessarily view now |
| **Audience snapshot** | Authorization record captured at publication governing historical access |
| **Trigger-post exception** | Token redemption grants trigger post and future eligible posts, never back catalog |
| **Revocation** | Invalidates future access/unused tokens after remove, block, deletion, expiry, or verification failure |
| **Server-private** | Access-controlled, encrypted-at-rest platform storage; not E2EE at MVP |
| **External write** | User-approved export of native public material to an external destination |
| **Private egress** | Unauthorized transfer of private content/metadata to an external endpoint; prohibited |
| **Qualified incident** | Incident meeting a formal hard-stop, feature-pause, trend-gate, or monitoring definition |
| **Confirmed unintended private-content exposure** | Confirmed unauthorized private read, private egress, evaluator grant outside intended audience, or privileged access outside approved audited path. It excludes recipient screenshots/voluntary sharing, correctly displayed-policy misunderstanding, and non-sensitive metadata issue without unintended disclosure. |
| **Unauthorized private-content access** | Successful retrieval of private content by an identity not authorized under the publication snapshot and applicable policy |
| **Confirmed exploit** | Unauthorized access demonstrated in production or production-equivalent environment |
| **Critical credible vulnerability** | No exposure confirmed, but exploitation is realistically plausible and requires immediate mitigation or feature freeze based on severity |
| **Policy snapshot** | Immutable capture of policy fields used to evaluate a published post |
| **Publication snapshot** | Policy snapshot, audience snapshot, and authorization timestamp bound to a post |
| **Policy evaluation** | One authorization/discovery/distribution decision for actor, post, action, and time |
| **Explanation code** | Stable evaluator reason for UI and audit use; never free-form topology inference |
| **Consent scope** | Exact context, category, community, purpose, and duration covered by consent |
| **Adapter provenance** | Source adapter, external ID, import time, freshness, and conversion history tied to imported data |
| **Safety override** | Narrow, audited suppression/restriction imposed by defined safety/legal process |
| **Stale-policy warning** | UI notice that a preset, charter, or adapter-derived candidate no longer reflects current rules/data |
| **Operator override** | Controlled, audited departure from ordinary community moderation workflow |

## Community and Economic Terms

| Term | Definition |
|---|---|
| **Community** | Chartered space with purpose, roles, norms, moderation, bridge defaults, and appeal path |
| **Community operator** | Charter-limited steward; no private-post/audience access by default |
| **Creator net payable** | Amount owed after disclosed direct costs, fees, refunds/chargebacks, and split rules |
| **Company retained revenue** | Platform revenue after creator/collaborator liabilities; only this enters company expense/reserve/surplus accounting |
| **Community fund** | Explicitly sourced and governed pool, not implied profit share |
| **Portability** | Export of own records and consent-respecting relationship metadata, never others’ private data |
| **Meaningful interaction** | Relationship-formation outcome: accepted introduction, durable mutual follow, substantive reciprocal exchange, or completed project action |