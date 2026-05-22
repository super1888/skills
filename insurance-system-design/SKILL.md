---
name: insurance-system-design
description: Use when designing, reviewing, or implementing insurance-related product systems, especially e-commerce insurance such as return shipping insurance, embedded insurance, policy issuance, claims, premium calculation, insurer/channel integration, compensation rules, risk controls, billing, reconciliation, or domain modeling for insurance workflows.
---

# Insurance System Design

Use this skill to design implementation-ready insurance systems from business requirements. It distills the design logic of Youzan's insurance system article into reusable guidance for modeling insurance products, policy issuance, claims, insurer channels, billing, and operational risk controls.

## Skill Positioning

- Applicable scenarios: e-commerce insurance, embedded insurance products, return shipping insurance, order-linked protection, policy/claim/settlement workflows, insurer channel integration.
- Core purpose: turn insurance business rules into clear domain boundaries, executable state flows, APIs, storage design, and validation checks.
- Task scope: product modeling, policy issuance, premium calculation, claim processing, channel routing, insurer callback handling, billing/reconciliation, risk and compensation design.
- Target users: backend engineers, architects, product analysts, and agents drafting insurance system designs.
- Non-goals: actuarial pricing models, legal interpretation of insurance clauses, insurer-side core system implementation, and regulatory compliance advice.

## Underlying Thinking

- Insurance capability should be modeled as a domain service around product, policy, claim, channel, billing, and risk control instead of being embedded directly in order or after-sales code.
- E-commerce insurance often starts from a concrete scenario, but the system should abstract reusable product rules, coverage periods, insured objects, premium calculation, and claim conditions.
- Policy issuance and claims are separate lifecycles. Keep policy status, claim status, payment/settlement status, and after-sales status independent but correlated by business keys.
- External insurer channels introduce uncertainty. Design idempotent requests, callback logs, retry strategies, reconciliation, and fallback states from the start.
- Use configuration to separate product rules from execution flows: product definition, merchant eligibility, SKU/order binding, premium rules, compensation limits, and channel strategy.
- Critical flows need audit records: policy creation, underwriting result, premium deduction, claim submission, claim review, insurer callback, compensation payment, and reconciliation differences.

## Practical Method

1. Identify the scenario and insured object: order, order line, shipment, after-sales request, merchant, buyer, or another business entity.
2. Define insurance product rules: coverage scope, insured amount, premium source, coverage period, claim trigger, exclusions, compensation cap, and effective/expiration conditions.
3. Split domain boundaries: product configuration, policy issuance, claim processing, channel integration, billing/reconciliation, risk control, and operations.
4. Design state machines before tables and APIs: policy lifecycle, claim lifecycle, channel request lifecycle, billing/reconciliation lifecycle.
5. Define idempotency keys and correlation keys: order ID, order item ID, policy number, claim number, insurer transaction number, after-sales ID, and settlement batch ID.
6. Design insurer channel abstraction: routing strategy, request adapter, response mapping, callback verification, retry, timeout, manual repair, and channel capability differences.
7. Persist audit and snapshot data: product rule snapshot, policy snapshot, premium calculation detail, claim evidence, compensation result, callback payload digest, and operator logs.
8. Add risk controls: repeated issuance, repeated claim, invalid after-sales status, stale order snapshot, channel timeout, premium mismatch, compensation over-limit, and reconciliation difference.
9. Produce artifacts in this order: assumptions, domain model, state machines, APIs/events, tables, channel integration, risk controls, validation checklist.

## Trigger Conditions

- Use when the user asks to design insurance, warranty, protection, freight insurance, return shipping insurance, claim, policy, insurer integration, premium, or compensation workflows.
- Strong trigger phrases: “保险系统设计”, “退货包运费”, “运费险”, “保单”, “理赔”, “出险”, “承保”, “保险渠道”, “保费计算”, “保险对账”, “嵌入式保险”.
- Domain keywords: insurance product, policy, claim, premium, coverage, insurer, underwriting, callback, settlement, reimbursement, risk control, reconciliation.
- Do not use when the task is only about generic payment, generic order fulfillment, legal compliance, actuarial modeling, or unrelated financial products.
- If the requirement lacks product rules or claim conditions, ask for insured object, trigger event, premium payer, compensation target, and insurer integration mode.

## Output Format

When using this skill, respond with:

- **Business Context**: scenario, insured object, actors, assumptions, and non-goals.
- **Domain Model**: bounded contexts, aggregate roots, key entities, snapshots, and correlation keys.
- **State Machines**: policy, claim, channel request, and billing/reconciliation states with guarded transitions.
- **Core Flows**: policy issuance, claim submission/review, insurer callback, compensation, retry, and manual repair paths.
- **APIs And Events**: command/query APIs, events, idempotency keys, permission scope, and callback verification.
- **Storage Design**: tables, unique keys, indexes, status fields, snapshots, audit logs, and reconciliation records.
- **Risk Controls**: duplicate issuance, duplicate claim, stale data, premium mismatch, compensation over-limit, channel failure, and reconciliation differences.
- **Validation Checklist**: test cases for boundary values, duplicate callbacks, channel timeout, retry, rollback, and manual operation.

## Reference Index

- Read `references/source-map.md` for source traceability and mapping from the Youzan article to this skill.
- Read `references/extraction-notes.md` for deeper domain decomposition, design rationale, and implementation trade-offs.
- Read `references/workflow-checklist.md` when drafting APIs, state machines, storage, risk controls, or validation cases.
- Read `references/examples.md` for representative prompts and expected output structure.
