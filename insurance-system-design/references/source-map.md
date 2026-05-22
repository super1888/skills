# Source Map

## Sources

| ID | Title | URL/File | Author/Org | Date | Notes |
| --- | --- | --- | --- | --- | --- |
| S1 | 保险系统的分析与设计 | https://tech.youzan.com/analysis_and_design_of_insurance_system/ | 有赞技术 | 2021-09-13 | Uses return shipping insurance as an entry point to discuss insurance system analysis and design. |

## Source To Skill Mapping

| Source ID | Key Idea | Distilled Skill Rule | Skill Location |
| --- | --- | --- | --- |
| S1 | Insurance is introduced through an e-commerce return shipping scenario. | Start with scenario and insured object, then abstract reusable insurance product capabilities. | `SKILL.md` / Skill Positioning, Practical Method |
| S1 | The article separates business analysis from system design. | Generate outputs in ordered artifacts: assumptions, domain model, states, APIs, tables, risks, validation. | `SKILL.md` / Practical Method, Output Format |
| S1 | Insurance products involve product rules, policy issuance, claims, channels, and billing. | Model product, policy, claim, channel integration, billing/reconciliation, and risk control as distinct boundaries. | `SKILL.md` / Underlying Thinking |
| S1 | External insurance companies and channels create integration uncertainty. | Require idempotent channel requests, callback logs, retry, timeout handling, and reconciliation. | `SKILL.md` / Practical Method, Risk Controls |
| S1 | The system needs to support business configuration and operational management. | Keep product rules, eligibility, premium rules, coverage, and channel routing configurable and auditable. | `references/extraction-notes.md` |

## Design Logic

- Problem the source solves: how to analyze and design an insurance system for e-commerce scenarios such as return shipping insurance.
- Key architectural idea: start from concrete business scenes, then abstract common insurance capabilities and independent lifecycles.
- Important constraints: insurer channel integration, state consistency, idempotent callbacks, premium/compensation correctness, and operational repair.
- Trade-offs: scenario-specific speed versus reusable product/channel abstractions; synchronous user experience versus asynchronous insurer confirmation.
- Failure modes: duplicate policy creation, repeated claims, stale order or after-sales data, insurer timeout, callback replay, and reconciliation mismatch.

## Traceability Notes

- The skill paraphrases and reorganizes the article's ideas rather than copying original text.
- The source article is used as conceptual inspiration for e-commerce insurance system design.
- Regulatory, legal, and actuarial details are intentionally outside the generated skill scope.
