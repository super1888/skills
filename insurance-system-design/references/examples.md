# Examples

## Prompt 1

帮我设计一个电商退货运费险系统，买家下单时由商家赠送，售后退货成功后自动理赔。

Expected output:

- Business Context
- Domain Model
- State Machines
- Core Flows
- APIs And Events
- Storage Design
- Risk Controls
- Validation Checklist

## Prompt 2

我们要接入多个保险公司的嵌入式保险产品，请设计保单出单、保险公司回调、对账和失败补偿方案。

Expected focus:

- Channel abstraction
- Idempotent policy application
- Callback verification
- Retry and manual repair
- Premium and settlement reconciliation

## Prompt 3

审阅这个理赔流程有没有风险：用户提交售后后，前端传理赔金额，后端直接打款。

Expected focus:

- Server-side claim amount calculation
- Policy and after-sales status guards
- Duplicate claim prevention
- Compensation cap validation
- Audit and reconciliation records
