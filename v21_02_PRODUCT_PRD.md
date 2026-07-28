# Product Requirements Document

**Project:** Social Distance as Interface  
**Version:** v21  
**Owner:** Product Lead  
**Readers:** Product, design, engineering, QA  
**Controls:** User behavior, states, UX copy, policy objects, acceptance criteria, MVP scope  
**Depends on:** `00_PRODUCT_CONSTITUTION.md`  
**Links:** Trust enforcement in `03_TRUST_SECURITY_SAFETY.md`; operations in `05_LAUNCH_OPERATING_PLAN.md`

## Product Goal

Enable users to share at an intentional distance, understand actual and potential reach, form consented connections, and exchange value without turning social life into a generic engagement feed.

## Core Policy Objects

A post policy contains separate backend objects for:

1. **Audience:** who may receive it now
2. **Reach:** who may encounter it later
3. **Distribution:** reshare, recommendation, introduction, and external-copy permissions
4. **Time:** expiry, review date, scheduled release, or gradual expansion
5. **Economic terms:** access, rights, and contributor allocations when applicable

These are distinct in storage and evaluation even when a named compose mode supplies safe defaults.

## Compose UX: Modes First, Controls on Demand

**UX principle:** every advanced control has a safe, understandable default. Users begin with named modes and expand policy detail only when needed.

| Mode | Default policy summary |
|---|---|
| Private thought | Selected private audience; no forwarding; no discovery |
| Circle update | My circle; optional request-before-reshare |
| Community post | Named community; community charter rules |
| Opportunity | Context-qualified bridge discovery; no public indexing |
| Public work | Followers/Open network; optional selected monetization |
| Gradual release | Starts small; expands only under author-defined conditions |

Default compose shows three primary choices: **Private audience**, **My network**, and **Open**. “Choose reach” reveals community, opportunity, gradual-release, discovery, distribution, time, and economic controls. Contextual community posting automatically offers that community’s mode.

### Required Compose Inputs

- Audience / current recipients
- Discovery/reach policy
- Distribution/reshare rule
- Time policy
- Destination: native Open network and optional adapters
- Economic terms when relevant
- Plain-language policy summary before publish

### Required Pre-Publish Preview

- “12 can see this now” for current audience
- “Up to about 112 may encounter it through opted-in community discovery” only when anonymity thresholds permit
- “Cannot be forwarded” / “Ask before sharing” / “May travel one additional degree with attribution”
- “Expires in 30 days” / “Review on [date]” / “Starts in your circle and may expand under this rule”
- External-destination disclosure and explicit acknowledgment if applicable

## Visibility and Discovery Rules

### Audience vs Reach

Audience determines immediate authorization. Reach determines later eligibility. A recipient does not gain immediate access merely because the post is eligible for future discovery.

### Bridge Consent

Friends-through-friends and opportunity discovery require:

- Author policy allowing bridge-based discovery
- Potential recipient opt-in
- Eligible context: community, topic, location, or project
- Minimum anonymity/crowd threshold
- Community safety rules

Bridge paths do not disclose an intermediary identity or exact degree unless all affected people have consented. A bridge never implies endorsement.

### Slow Travel

Slow travel is a time-based distribution policy, not a reach level.

- Starts with an author-selected audience or community
- Expands only at a pace selected by the author
- Requires signals defined by the author/policy that are not raw likes alone
- Honors recipient consent, context rules, and safety thresholds
- May be paused, narrowed, or withdrawn by the author
- Maintains a visible distribution history for the author
- Never expands into a platform-wide viral feed by default

## Private Audience Model

A private audience is an explicit authorization list for a specific post or reusable preset. Presets are convenience; post-specific editing is always visible.

### Recipient States

| State | Meaning | Can view a private post now? |
|---|---|---|
| Not followed | No follow relationship | No |
| Followed | Sees eligible feed content | No |
| Audience member, uninvited | Authorized in a preset/post but not yet invited | No unless already active member |
| Invited, link valid | Unique invite token exists | No |
| Invite opened | Token viewed; signup incomplete | No |
| Joined / active | Token redeemed / active account | Yes, if in post snapshot or trigger exception |
| Removed | Future authorization revoked | No |
| Blocked | Access and interaction revoked | No |
| Account deleted | Deleted-account policy applies | No |

### Private-Post Acceptance Criteria

- A follow cannot enter a private audience without a distinct user confirmation.
- Compose must show current viewers separately from invited recipients.
- Post creation stores audience snapshot, policy snapshot, and authorization timestamp.
- A recipient added after creation cannot retrieve prior content except through a matching valid trigger-post invitation.
- Remove/block invalidates future access immediately.
- User-facing private-post copy: “Private to your selected audience; stored encrypted on our servers; not end-to-end encrypted yet.”

## Pairwise Invite State Machine

1. Author adds a person to a private audience.
2. System creates a unique, single-recipient invitation token only when author elects to invite.
3. Author shares copy link through a chosen channel.
4. Recipient may open, report, block, verify identity, sign up, or abandon.
5. On valid redemption, native account links to that audience entry; status becomes Joined/active.
6. Recipient receives the trigger post and future posts including the audience entry.
7. Author remove/block/delete, recipient block, token expiry, or verification failure revokes remaining token access.

### Invite Acceptance Criteria

- Tokens are unique, recipient-bound, expire/revoke correctly, and cannot activate a mismatched account.
- Forwarded links require recipient verification and cannot silently grant access.
- Invitees can report or block before signup.
- Invite copy is accurate: “Join to view this post and future posts [author] shares with this audience.”
- One invitation is sent per audience addition, not per later private post.
- Rate limits and quiet hours are enforced.

## Feed and Ranking

The native Following feed is primary. It can include permitted adapter content as a user-selected enrichment source.

### Feed Policies

- Chronological
- Close relationships first
- New voices first
- Local/community first
- Topic-specific
- Creator-supporting mode
- No recommendations
- Serendipity mode with stated exploration budget

Every ranked item provides “Why am I seeing this?” Users can change the policy or reset it.

### Relationship Memory

Recency may rank content but never narrates relationship quality. The UI uses neutral evidence on request (“Last interacted 8 months ago”), supports pin/mute/important overrides, and does not call a relationship “decayed.” Imported interaction data requires consent and cannot create authorization or rights.

## Discovery and Connection

### Objects

- Request an introduction with purpose
- Looking-for cards
- Project rooms
- Community vouches
- Limited weekly high-quality introductions

### Interaction Modes

| Mode | Destination | Requirement |
|---|---|---|
| Public reply | Native Open network and optional adapter destinations | Destination disclosure and confirmation |
| Private note | Native only, to author/selected members as specified | Never an external write |
| Request introduction | Consent-gated recipient workflow | Does not grant private access |

Following after an introduction creates a native follow. External following may be offered only as a separate optional adapter action.

## Communities

Communities require a charter defining purpose, membership, roles, moderation, bridge/discovery defaults, operator permissions, appeal path, and any fund/participation rules.

Operators cannot view private posts, private-audience membership, or private interaction data by default. Permissions are visible, minimum necessary, and auditable.

## Creator Commerce Objects

The product model supports, over time:

- Tips
- Pay-what-you-want posts/digital goods
- One-time purchases
- Memberships
- Revenue splits
- Community funding
- Licensing and rights rules
- Events, bounties, and projects

**MVP commerce stack:** tips, pay-what-you-want digital work, named collaborator splits, a transparent earnings ledger, and community-fund allocation visibility. Ads, rentals, bundles, subscriptions, tickets, complex licensing, and advanced tax workflows are deferred.

## Critical UX Copy

- Private post: “Private to your selected audience; stored encrypted on our servers; not end-to-end encrypted yet.”
- Invite: “Maya shared a private post with you. Join to view this post and future posts she shares with this audience.”
- External reply: “This reply will be public on the selected destination(s) and subject to their policies.”
- Bridge discovery: “Shown through your network and shared community context.”
- No intermediary disclosure: “Through your network” rather than a named path when consent is absent.

## Must Ship

- Native identity and follows
- Private posts, post-level audiences/presets, delivery counts, invitation/revocation/snapshots
- Native Following feed and basic user-controlled ranking
- One bounded discovery path in opt-in communities
- Native Open posting; external cross-post as optional adapter
- Three interaction modes
- Block/report/rate limiting/invite-abuse controls
- Essential notification and event instrumentation

## Deferred

- Native DMs
- Broad unbounded discovery
- Reposts and general search
- Complex decay UI
- Broad commerce catalog beyond MVP stack
- Formal participant revenue-share/governance implementation

## Changelog

- **v21:** Extracted from v20; adds progressive disclosure, distinct policy objects, slow-travel definition, and concrete MVP commerce cut.