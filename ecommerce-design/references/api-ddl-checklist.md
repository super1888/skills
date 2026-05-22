# API And DDL Checklist

## API Design

For each API, define:

- Actor and scope: buyer, merchant, platform admin, warehouse, finance, system callback.
- Business key: orderNo, payNo, refundNo, couponNo, reservationNo, shipmentNo.
- Idempotency key: client request ID, third-party transaction ID, or unique business command key.
- Permission guard: tenant ID, merchant ID, store ID, user ID, platform role.
- Validation: status guard, amount guard, ownership guard, time window, quantity/stock limit.
- Response: stable code, user-actionable message, current status, and next operation hints when useful.

## DDL Design

Every critical commerce table should consider:

- Primary key plus immutable business number.
- `tenant_id` or `merchant_id` if multi-tenant or marketplace.
- Status fields with clear enum definitions.
- Amount fields in integer cents unless the project standard says otherwise.
- Snapshot JSON/text for historical display when upstream data can change.
- `created_at`, `updated_at`, `created_by`, `updated_by` where applicable.
- Unique indexes for idempotency: orderNo, payNo, channelTxnNo, refundNo, couponNo.
- Composite indexes for common lists: user+createdAt, merchant+status+createdAt, order+item, SKU+status.

## Events

Typical events:

- ProductPublished, ProductUnpublished, SkuPriceChanged, SkuStockChanged.
- CartCheckedOut, OrderCreated, OrderCanceled, OrderPaid, OrderShipped, OrderCompleted.
- PaymentRequested, PaymentSucceeded, PaymentFailed, RefundSucceeded.
- StockLocked, StockDeducted, StockReleased, StockRollbackRequested.
- CouponClaimed, CouponLocked, CouponUsed, CouponReleased.

Event rules:

- Include event ID, occurred time, aggregate ID, source service, and version.
- Consumers must be idempotent.
- Prefer outbox or transaction log for events coupled to database writes.

## Concurrency Patterns

- Atomic stock deduction: `update sku_stock set available = available - ? where sku_id = ? and available >= ?`.
- Optimistic version: use for product edits and campaign configuration.
- Unique constraint: use for duplicate create/payment/refund prevention.
- Distributed lock: use sparingly for hot campaigns; still keep database guards.
- Timeout job: releases unpaid orders, expired stock locks, and locked coupons.

## Test Checklist

- Duplicate submit order, duplicate payment callback, duplicate refund callback.
- Price changed after cart add, SKU disabled after cart add, stock insufficient at checkout.
- Coupon expired between checkout and payment, campaign quota exhausted under concurrency.
- Payment success after user cancel attempt, cancel after payment success, stale callback after close.
- Partial shipment, partial refund, refund after shipment, refund exceeding paid amount.
- Merchant isolation, tenant isolation, unauthorized platform operations.
