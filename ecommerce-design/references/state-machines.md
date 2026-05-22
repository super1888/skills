# State Machines

## Order

Recommended separate dimensions:

- `orderStatus`: CREATED, CONFIRMED, CANCELED, CLOSED, COMPLETED.
- `payStatus`: UNPAID, PAYING, PAID, PARTIAL_REFUNDED, REFUNDED.
- `fulfillmentStatus`: WAIT_SHIP, PARTIAL_SHIPPED, SHIPPED, RECEIVED.
- `afterSaleStatus`: NONE, APPLYING, PROCESSING, DONE, REJECTED.

Key transitions:

- Create order: cart/checkout validation passes, amount snapshot is persisted.
- Cancel unpaid order: release locked stock and coupon, write operation log.
- Pay success: verify amount and channel transaction, mark paid, trigger stock/failure compensation strategy.
- Ship: verify paid and not fully refunded, create shipment and delivery events.
- Receive/complete: verify shipment status, close after-sales window by configured rule.

## Payment

Statuses: INIT, REQUESTED, SUCCESS, FAILED, CLOSED, REFUNDED, PARTIAL_REFUNDED.

Guards:

- Unique business payment number.
- Unique channel transaction number when callback provides one.
- Callback amount equals payable amount.
- Final states cannot be overwritten by stale callbacks.

## Refund / Return

Statuses: APPLIED, APPROVED, REJECTED, WAIT_RETURN, RETURNED, REFUNDING, REFUNDED, CLOSED.

Guards:

- Refundable amount = paid amount - successful refund amount - refunding amount.
- Refundable quantity = purchased quantity - successful/refunding return quantity.
- Refund payment should be independent from approval so finance/channel failures can retry.

## Inventory

Recommended dimensions:

- `availableStock`: can be sold.
- `lockedStock`: reserved for unpaid or pending orders.
- `soldStock`: paid or shipped depending on policy.

Common modes:

- Lock at order creation, deduct at pay success, release on cancel/payment timeout.
- Deduct at pay success using atomic conditional update for flash-sale or low-stock scenarios.
- Pre-sale mode records promised quantity separately from physical stock.

## Coupon

Statuses: UNCLAIMED, CLAIMED, LOCKED, USED, EXPIRED, RELEASED, INVALID.

Guards:

- Claim limit by user, activity, period, and total budget.
- Lock during order creation when coupon participates in amount calculation.
- Use on payment success or order creation depending on business rule; always provide rollback/release on cancel.

## Promotion Campaign

Statuses: DRAFT, SCHEDULED, RUNNING, PAUSED, ENDED, ARCHIVED.

Guards:

- Campaign time window and product scope must be immutable or versioned after running.
- Budget/quota deduction must be atomic.
- Rule evaluation should record calculation details for customer service disputes.
