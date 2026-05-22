---
name: ecommerce-design
description: Use when designing, reviewing, or implementing e-commerce product requirements, domain models, APIs, workflows, database tables, state machines, or frontend/backend modules for commerce systems; covers SKU/SPU, cart, order, payment, inventory, promotion, coupon, after-sales, membership, settlement, and merchant/platform boundaries.
---

# E-commerce Design

Use this skill to turn e-commerce requirements into implementation-ready designs. It distills common patterns from `skr-shop/manuals` and general commerce architecture practices without copying source text.

## Core Workflow

1. Identify the business scene: buyer, merchant, platform, operator, warehouse, finance, or support.
2. Locate the domain boundary: catalog, marketing, cart, trade, payment, inventory, fulfillment, after-sales, user, settlement, or search.
3. Define state machines before tables and APIs. Commerce bugs often come from unclear status transitions.
4. Split write paths from read/query paths when listings, search, or order histories need denormalized views.
5. Design idempotency, concurrency control, and compensation for every money, stock, coupon, or order mutation.
6. Produce artifacts in this order: assumptions, domain model, state transitions, APIs/events, tables, edge cases, validation plan.

## Load References As Needed

- Read `references/domain-map.md` when choosing module ownership, bounded contexts, or aggregate roots.
- Read `references/state-machines.md` when designing order, payment, refund, coupon, inventory, or logistics status.
- Read `references/api-ddl-checklist.md` when drafting APIs, tables, indexes, events, locks, or validation rules.

## Design Principles

- Use `SPU` for product identity and shared selling content; use `SKU` for purchasable variants, price, stock, and attributes.
- Treat order, payment, refund, stock deduction, coupon usage, and points changes as auditable business records.
- Never rely on frontend price, discount, freight, stock, or permission values; recalculate server-side.
- Persist snapshots for order lines: product title, SKU attributes, image, price, promotion details, merchant, and freight info.
- Prefer append-only logs for critical flows: order operation log, payment callback log, stock movement log, refund audit log.
- Make external callbacks idempotent with business keys, third-party transaction IDs, unique constraints, and status guards.
- Reserve stock before payment only when the scenario needs it; otherwise deduct at payment with oversell protection.
- Separate promotion eligibility calculation from promotion usage/write-off to avoid locking long calculation paths.
- Keep platform, merchant, and tenant permissions explicit in every management API.

## Required Output Shape

When asked for a design, include:

- Business assumptions and non-goals.
- Domain boundaries and aggregate roots.
- Main happy path plus failure/compensation paths.
- State machine tables or diagrams.
- API list with request keys, idempotency keys, and permission scope.
- Storage design with unique keys, indexes, status fields, and audit logs.
- Concurrency/risk notes: oversell, repeated payment, repeated refund, stale price, coupon race, inventory rollback.
- Test checklist covering boundary values and duplicate callbacks.

## Common Red Flags

- One status field mixes payment, fulfillment, refund, and close states.
- Order amount is updated without a recalculation record.
- Payment callback updates order directly without idempotency or amount verification.
- Coupon is marked used before order creation is guaranteed, with no rollback path.
- Inventory is stored only on SKU with no stock movement ledger.
- Refund succeeds without checking paid amount, refundable amount, and existing refund records.
- Product updates mutate historical order displays instead of using order snapshots.
- Merchant APIs can access platform/global records without tenant constraints.

## Source Inspiration

Reference project: https://github.com/skr-shop/manuals
Use it as conceptual inspiration for commerce domains such as accounts, cart, order, promotion, payment, stock, and after-sales. Do not paste large verbatim content from the source.
