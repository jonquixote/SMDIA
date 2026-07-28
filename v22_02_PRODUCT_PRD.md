# Product Requirements Document

**Project:** Social Distance as Interface  
**Version:** v22  
**Owner:** Product Lead  
**Readers:** Product, design, engineering, QA  
**Authority level:** Binding specification  
**Changes require:** Product + engineering review; security review for authorization/external-write changes  
**Review cadence:** Monthly, before launch gate, and after relevant SEV-0/SEV-1 incident  
**Conflicts resolved by:** `00_PRODUCT_CONSTITUTION.md`  
**Last cross-document consistency review:** 2026-07-27

## Purpose

Define what a user does, sees, controls, and understands. This is a modular product contract: each feature must identify its user problem, promise, states, authorization, events, acceptance criteria, linked constitutional rules, linked security invariants, owner, and open questions.

## Canonical Domain Model: `PostReachPolicy`

Every post stores a versioned `PostReachPolicy`:

```text
PostReachPolicy
- immediate_audience
- discovery_eligibility
- distribution_rights
- reshare_policy
- time_policy
- destination_policy
- economic_policy
- rights_policy
- safety_constraints
- policy_version
```

Definitions:

- **Audience:** who can retrieve it now
- **Reach:** who may encounter it later under policy
- **Distribution:** how it may move
- **Discovery:** whether a relationship opportunity may be created
- **Bridge consent:** whether a person permits their graph position to support a qualifying path

Preview and actual delivery call the same versioned policy evaluator. A preview can be coarsened for privacy; it never overstates present or future eligibility. Implements `CONST-GRAPH-003` and `CONST-TRUST-001`.

## Compose Experience

### Default choices

First-time/default compose presents only:

1. **Private audience**
2. **My network**
3. **Open**

“Choose reach” reveals advanced choices only when useful. Friends-through-friends appears only when bridge consent and context make it eligible. Commerce terms appear only for eligible post types. The system remembers safe prior choices by mode/preset.

### Advanced dimensions

| Dimension | User question | Examples |
|---|---|---|
| Immediate audience | Who receives this now? | Only me, selected audience, circle, community, followers, everyone |
| Discovery eligibility | Who may encounter it later? | Nobody, selected community, consent-qualified network, shared-context discovery |
| Travel rule | How may it move? | No forwarding, ask before sharing, reshare with attribution, one additional degree |
| Time rule | How long does the policy apply? | Permanent, expire, review date, scheduled release, gradual expansion |
| Economic terms | How is access paid? | Free, tips, PWYW, price, subscriber-only |
| Rights | What reuse is allowed? | Personal viewing, educational license, remix, no AI training |

### Modes

| Mode | Generated policy |
|---|---|
| Private thought | Selected audience; no discovery; no forwarding |
| Circle update | Direct network; controlled reshare |
| Community post | Community audience and charter rules |
| Opportunity | Context-qualified bridge discovery; no public index by default |
| Public work | Followers/Open network; optional commerce |
| Gradual release | Starts small; expands only under author-defined consent/safety conditions |

## Feature: Private Audience Posting

**User problem:** A user needs to share candidly with people they choose while knowing who can actually receive it.

**Promise:** “You can see who can view this now, and the system enforces the policy you selected.”

**Non-goals:** E2EE at MVP; preventing screenshots; importing followers as automatic recipients.

**Actors:** Author, active recipient, invitee, report reviewer, security responder.

### Recipient states

Not followed; followed; audience member/uninvited; invited/link valid; invite opened; joined/active; removed; blocked; account deleted.

### Primary flow

1. Author selects post-specific audience or preset.
2. Compose displays active recipients separately from invitees.
3. Author publishes; system saves policy and audience snapshot.
4. Active recipients can retrieve according to snapshot/policy.
5. Invitees require valid token redemption.

### Authorization rules

- Follow does not grant private access (`CONST-GRAPH-002`).
- Post-time snapshot governs historical access (`CONST-TRUST-002`).
- Remove/block/delete revokes future access (`CONST-TRUST-003`).
- Private records are server-private, encrypted at rest, and not E2EE at MVP.

### Analytics events

`private_post_composer_opened`, `private_audience_selected`, `private_post_published`, `delivery_count_viewed`, `audience_policy_edited`, `private_post_viewed`, `private_post_access_denied`.

### Acceptance criteria

- Compose separately displays “can see now” and “invited.”
- No inactive invitee can retrieve a private post.
- A later-added recipient cannot fetch older content without matching trigger-token exception.
- Private post UI says: “Private to your selected audience; stored encrypted on our servers; not end-to-end encrypted yet.”

## Feature: Pairwise Invite

**User problem:** An author needs to invite a person into a private relationship without lying about current delivery.

**Promise:** “Join to view this post and future posts I share with this audience.”

**State model:** created -> shared -> opened -> verified -> redeemed/joined; terminal states revoked, expired, blocked, deleted.

**Primary flow:** Author elects invite -> unique recipient-bound token created -> author shares link -> invitee verifies/signs up -> entry flips to active -> trigger post + future authorized posts become available.

**Edge cases:** forwarded link, duplicate account, opened-but-unfinished signup, author removal, invitee block/report, token expiry, author deletion.

**Authorization:** Token grants only trigger post plus future authorized posts; no back catalog.

**Analytics:** `invite_created`, `invite_shared`, `invite_opened`, `invite_verified`, `invite_redeemed`, `invite_revoked`, `invite_reported`, `invite_blocked`.

**Acceptance criteria:** recipient binding; verification; one-time-per-audience-addition notification; rate limits/quiet hours; pre-signup report/block; correct revocation. Implements `CONST-TRUST-001` through `003`.

## Feature: Post Lifecycle

| State | Retrieval / notices / economic behavior |
|---|---|
| Draft | Author only; no notifications or external copies |
| Scheduled | Author only until publish; policy may be edited |
| Published | Policy evaluator controls retrieval/discovery/distribution |
| Policy changed for future access | New policy applies prospectively; immutable audit/policy history retained |
| Expired | No ordinary retrieval; author/audit/export rules apply; paid access follows stated entitlement policy |
| Archived | Not surfaced by default; authorization remains policy-defined |
| Deleted | Live retrieval removed; deletion/backup/legal-hold policy applies |
| Under report/review | Access unchanged unless safety action restricts it; report scope controls reviewer evidence |
| Access restricted | Specific audience/distribution constraints modified under documented safety/legal process |
| Exported | Export event logged; export does not alter access |
| Cross-post pending/succeeded/failed | Native post remains canonical; external status shown; retry/cancel follows destination policy |

## Feature: Discovery and Introductions

**User problem:** People need relevant connections without public performance, invisible graph mining, or unwanted exposure.

**Promise:** “Meet people through context and consent—not through a hidden engagement feed.”

**Objects:** request-introduction, Looking For card, project room, community vouch.

**Rules:** bridge consent is explicit/scope-specific; no intermediary identity/degree disclosure without required consent; minimum crowd thresholds; introduction does not grant private access.

**Interaction modes:** public reply, private note, request introduction. Public reply requires destination disclosure; private note never externally writes; request introduction is recipient-consented.

**Analytics:** `bridge_consent_changed`, `introduction_requested`, `introduction_accepted`, `introduction_declined`, `mutual_follow_created`, `context_discovery_impression`, `topology_protection_triggered`.

## Feature: Feeds and Meaningful Interaction

Users choose chronological, close-first, new-voices, local/community, topic, creator-supporting, no-recommendations, or explainable serendipity modes. “Why am I seeing this?” reveals an editable, resettable policy.

**Meaningful-interaction definitions:**

- **Second private post:** another private post published at least 24 hours after the first.
- **Accepted introduction:** recipient accepts a request and both parties receive the connection path.
- **Mutual follow:** two native follow edges remain active for at least 24 hours.
- **Substantive reply exchange:** at least two reciprocal replies across two participants over at least 24 hours; raw reply count alone does not qualify.
- **Paid support:** completed, non-refunded payment after the refund-risk window.
- **Project participation:** a user completes a defined project-room action, not merely joins.

Blocked/removed relationships do not count after removal; metrics retain anonymized historical event records only as permitted by retention policy.

## Feature: Creator Commerce

MVP: tips, pay-what-you-want work, named collaborator splits, earnings ledger, community-fund visibility. Creator retains copyright by default; platform license is limited; no AI-training license without explicit opt-in. See `04_COMMERCE_OWNERSHIP.md`.

## Must Ship / Deferred

Must ship: native identity/follows; private posts/audiences/invites; native feed; one bounded discovery path; native Open posting; interaction modes; safety controls; event taxonomy.

Deferred: native DMs, broad discovery, reposts, general search, complex recency UI, broad commerce catalog, formal revenue sharing/governance implementation.

## Changelog

- **v22:** Adds `PostReachPolicy`, policy-evaluator requirement, feature templates, post lifecycle, and measurable interaction definitions.