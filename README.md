# The **Product Constitution** is the conflict-resolution authority: if documents disagree, follow it and record the resolution in `DECISIONS.md`.

## Read in this order

1. [Product Constitution](00_PRODUCT_CONSTITUTION.md) — binding invariants and conflict resolution
2. [Decisions Register](DECISIONS.md) — approved implementation and governance decisions
3. [Glossary](GLOSSARY.md) — canonical terms and required identifiers
4. [Product PRD](02_PRODUCT_PRD.md) — user-facing requirements and product scope
5. [Policy Evaluator Contract](POLICY_EVALUATOR_CONTRACT.md) — enforceable action-level authorization rules
6. [Launch Operating Plan](05_LAUNCH_OPERATING_PLAN.md) — gates, cohorts, scorecard, and expansion criteria

## Supporting documents

- [Vision Memo](01_VISION_MEMO.md)
- [Trust, Security, and Safety](03_TRUST_SECURITY_SAFETY.md)
- [Commerce and Ownership](04_COMMERCE_OWNERSHIP.md)
- [Integration Adapter Specification](06_INTEGRATION_ADAPTER_SPEC.md)
- [Open Questions](OPEN_QUESTIONS.md)
- [Traceability Matrix](TRACEABILITY_MATRIX.md)
- [Metrics and Event Taxonomy](METRICS_EVENT_TAXONOMY.md)

## Contributor rules

- Use the canonical identifiers exactly: `policy_id`, `policy_schema_version`, `evaluator_semantics_version`, `policy_snapshot_id`, `audience_snapshot_id`, and `publication_snapshot_id`.
- Do not add a user promise that the Policy Evaluator cannot enforce.
- Keep private-loop retention, relationship formation/meaningful interaction, and economic validation as separate scorecard dimensions.
- Link material behavior changes to a decision, traceability row, event definition, and evaluator test.