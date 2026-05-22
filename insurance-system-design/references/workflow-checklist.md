# Workflow Checklist

## Requirement Questions

- What is the insured object: order, order item, shipment, after-sales request, merchant, or buyer?
- Who pays the premium: buyer, merchant, platform, insurer subsidy, or mixed payer?
- What triggers coverage effectiveness and expiration?
- What event triggers a claim, and what evidence is required?
- Who receives compensation, and what is the maximum amount?
- Is an external insurer involved, and is policy issuance synchronous or asynchronous?

## Design Checklist

- Define product code, scenario code, rule version, and coverage snapshot.
- Define policy, claim, channel request, billing, and reconciliation state machines separately.
- Add unique constraints for policy issuance and claim creation by business object.
- Add idempotency keys for user commands, insurer requests, callbacks, and compensation operations.
- Store snapshots for order, after-sales, product rule, premium calculation, and claim amount.
- Add callback logs with signature result, payload digest, channel transaction number, and processing status.
- Add retry and manual repair flows for timeout, failed callback processing, and reconciliation differences.
- Add reconciliation by premium, compensation, insurer settlement, and merchant/platform accounting dimensions.

## API Checklist

- Policy apply API: validates eligibility, calculates premium, snapshots rule and insured object, returns policy application result.
- Policy query API: returns policy lifecycle and channel status without exposing raw insurer payload by default.
- Claim create API: validates policy status, claim trigger, evidence, duplicate claim, and compensation cap.
- Claim review/submit API: supports automated rule check and optional manual audit.
- Insurer callback API: verifies signature, validates business key, handles replay idempotently, and records raw callback safely.
- Reconciliation API: imports insurer settlement data, compares expected records, marks differences, and supports repair workflow.

## Test Checklist

- Duplicate policy apply for the same order item.
- Claim before policy effective, after policy expired, and after policy cancelled.
- Duplicate claim for the same after-sales request.
- Insurer callback replay, invalid signature, amount mismatch, unknown policy, and out-of-order callback.
- Channel timeout followed by late success callback.
- Premium rule version change after policy creation.
- Compensation cap boundary and zero/negative amount rejection.
- Reconciliation difference: missing insurer record, extra insurer record, amount mismatch, and repeated import.
