# Domain Map

## Catalog

- Aggregate roots: SPU, SKU, category, brand, attribute template.
- Key records: SKU sale attributes, SKU price, SKU stock reference, product audit record, product snapshot.
- Design notes: separate listing state from audit state; product detail reads can be denormalized; order lines must use snapshots.

## Cart

- Aggregate root: user cart or visitor cart.
- Key records: cart item, selected state, quantity, SKU version, price-at-view cache.
- Design notes: cart stores intent, not final price; checkout must revalidate SKU status, stock, price, freight, promotion, and purchase limits.

## Trade / Order

- Aggregate roots: order, order item, order package when split fulfillment exists.
- Key records: order amount detail, order operation log, order snapshot, order address snapshot.
- Design notes: separate order status, pay status, delivery status, and refund status unless a simple one-line order truly suffices.

## Payment

- Aggregate roots: payment order, payment channel transaction.
- Key records: payment request, payment callback log, payment reconciliation record.
- Design notes: verify amount, merchant/order ownership, channel status, duplicate callback, and already-finalized state.

## Inventory

- Aggregate roots: stock item, stock reservation, stock movement ledger.
- Key records: available stock, locked stock, sold stock, rollback record.
- Design notes: use atomic conditional update or optimistic version; keep a stock ledger for audit and compensation.

## Promotion

- Aggregate roots: campaign, promotion rule, coupon template, coupon instance.
- Key records: eligibility rule, usage record, budget/quota record, promotion calculation detail.
- Design notes: calculation can be stateless; write-off must be transactional and idempotent.

## Fulfillment

- Aggregate roots: shipment, package, delivery task.
- Key records: logistics company, tracking number, shipment item, delivery event.
- Design notes: support order splitting by merchant, warehouse, temperature, or logistics constraint.

## After-sales

- Aggregate roots: refund/return request, refund transaction.
- Key records: return item, evidence, audit record, refund payment record, logistics return record.
- Design notes: refundable quantity and amount must be derived from paid order items minus prior successful refunds.

## User / Membership

- Aggregate roots: account, member profile, address, points account.
- Key records: login identity, address snapshot, points ledger, growth value ledger.
- Design notes: account identity and membership benefits should be separated from order ownership.

## Settlement

- Aggregate roots: settlement bill, merchant account, commission rule.
- Key records: order settlement line, refund adjustment line, withdrawal record, reconciliation record.
- Design notes: settlement should use immutable order/payment/refund facts and generate auditable differences.

## Search / Recommendation

- Aggregate roots: search document, index task.
- Key records: product index, keyword stats, ranking config.
- Design notes: index asynchronously from catalog changes; do not treat search index as source of truth.
