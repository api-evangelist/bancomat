---
generated: '2026-09-17'
method: generated
name: Pay an Italian pagoPA notice
description: Upload a pagoPA payment notice (Numero Avviso + creditor PA VAT code) as a FlowPay document, open a checkout to pay it, track the pagoPA status machine and fetch the receipt.
api: openapi/bancomat-flowpay-api-v2-openapi.yml
operations: [pagopaPayment, getPagopaDetails, createCheckout, getPagopaReceipt]
source: >-
  operationIds verified in openapi/bancomat-flowpay-api-v2-openapi.yml; status machine from
  github.com/FlowPay/client-openapi/docs/pagopa_status.md and pagopa_lifecycle.md; domain
  standard recorded in conformance/bancomat-conformance.yml (domain_standards.pagopa).
---

# Pay an Italian pagoPA notice

pagoPA is the Italian public-administration payment platform; a notice is identified by its 18-digit `noticeNumber` and the creditor administration's `paVatCode`. FlowPay is a pagoPA PSP, so the notice becomes a FlowPay document that a checkout can pay.

## Auth
- Token with `pagopa:write` (upload) and `pagopa:read` (read/receipt). See `scopes/bancomat-scopes.yml`.

## Steps
1. **Upload the notice** — `pagopaPayment` (`POST /pagopa`) with required `noticeNumber` and `paVatCode`, optional `debtorVatCode`, `debtorMail`, `fee`. Expect `200` with `fingerprint`, `ec` (the creditor entity), `debtor`, `remittance`, `amount`, `status` = `ready`.
2. **Open a checkout** — `createCheckout` (`POST /checkout`) with `kind` = pagoPA document kind and the `fingerprint`; redirect the payer to the returned link.
3. **Track the status** — `getPagopaDetails` (`GET /pagopa/{fingerprint}`): `ready` → `activated` (payer started; "an activated payment notice cannot be paid by another payment provider until it is paid or unactivated") → `paid`. `locked` means another PSP activated it; `paidOnAnotherProvider` means the user paid elsewhere — stop.
4. **Fetch the receipt** — `getPagopaReceipt` (`GET /pagopa/{fingerprint}/receipt`) once `paid`.

## Idempotency / reversal
- Uploading the same notice twice is a duplicate document (v1 code 2012). There is no cancel for an activated notice in the contract; v1 allows `PATCH /pagopa/{fingerprint}` to edit an unpaid document. See `conventions/bancomat-conventions.yml` (reversibility).

## Errors
- `400` on a malformed notice number / VAT code (`additionalInfo.path`); `409` on state conflicts; `429` at 100 req/min per IP. See `errors/bancomat-problem-types.yml`.
