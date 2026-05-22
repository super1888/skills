# Extraction Notes

## Domain Decomposition

- **Product Configuration**: insurance product, coverage scope, premium rule, claim rule, effective period, merchant eligibility, channel strategy.
- **Policy Issuance**: policy application, underwriting request, policy number, effective state, premium charge, failure compensation.
- **Claim Processing**: claim trigger, evidence, claim amount, review rule, insurer claim request, compensation result, manual audit.
- **Channel Integration**: insurer adapter, request mapping, response mapping, callback verification, retry, timeout, capability differences.
- **Billing And Reconciliation**: premium records, compensation records, insurer settlement, merchant/customer billing, reconciliation difference handling.
- **Risk Control**: duplicate operations, status guards, fraud signals, eligibility check, compensation cap, manual override audit.

## Key Entities

- `InsuranceProduct`: product code, scenario, coverage, premium rule, claim rule, effective period, status.
- `InsurancePolicy`: policy number, product snapshot, insured object, applicant, insured party, premium, coverage period, status.
- `InsuranceClaim`: claim number, policy number, trigger object, claim reason, evidence, claim amount, status, compensation result.
- `InsuranceChannel`: insurer, channel product code, capability flags, routing priority, callback config, status.
- `ChannelRequestLog`: request type, business key, payload digest, response, retry count, channel transaction number.
- `PremiumRecord`: payer, amount, calculation detail, payment status, settlement status.
- `ReconciliationRecord`: settlement batch, expected amount, actual amount, difference type, repair status.

## State Separation

Avoid using one status to represent every lifecycle. Keep these state dimensions separate and correlated:

- Policy status: pending, applying, effective, failed, expired, cancelled.
- Claim status: created, reviewing, submitted_to_insurer, approved, rejected, paid, closed.
- Channel request status: initialized, sent, success, failed, timeout, retrying, manual_required.
- Billing status: pending, charged, refunded, settled, difference_found, repaired.

## Design Trade-offs

- If user experience requires immediate confirmation, return an internal accepted state and finish insurer confirmation asynchronously.
- If premium correctness matters more than speed, snapshot order and product rule details before charging or issuing.
- If multiple insurers are supported, normalize internal states and isolate insurer-specific payloads inside adapters.
- If business rules change frequently, keep product and claim rules configurable but snapshot the effective rule version on policies and claims.

## Common Red Flags

- Policy creation directly mutates order status without a business event or status guard.
- Claim processing depends only on frontend-provided amount or after-sales reason.
- Insurer callback updates policy or claim without signature verification, idempotency, or amount validation.
- Product rule changes alter historical policies because no snapshot or rule version is persisted.
- Premium, compensation, and settlement records are not reconcilable by unique business keys.
