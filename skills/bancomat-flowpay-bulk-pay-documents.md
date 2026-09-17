---
generated: '2026-09-17'
method: generated
name: Settle several documents with one SCA (bulk payment)
description: Aggregate invoices, bills and pagoPA notices a tenant owes into one FlowPay bulk document, pay it with a single strong-customer-authentication, and let FlowPay's technical account split the funds to each beneficiary.
api: openapi/bancomat-flowpay-api-v2-openapi.yml
operations: [getInvoices, createBulkPayment, createCheckout, getBulkPayment, deleteBulkPayment]
source: >-
  operationIds verified in openapi/bancomat-flowpay-api-v2-openapi.yml; mechanics from
  github.com/FlowPay/client-openapi/docs/bulk_lifecycle.md and fee_description.md.
---

# Settle several documents with one SCA (bulk payment)

A bulk document links many payable documents; the payer authorises ONE PIS transfer to FlowPay's technical account (TA), which splits it among the beneficiaries while each payment keeps the original payer/payee. **Not available in the public sandbox** (requires the TA) — request a dedicated sandbox (`sandbox/bancomat-sandbox.yml`).

## Auth
- `createBulkPayment` "does not require specific scopes, the authorization token used must have access to documents it wants to bulk pay" — so the token needs the read scopes of every linked document type (`invoices:read`, `bills:read`, `pagopa:read` ...).

## Steps
1. **Collect what is owed** — `getInvoices` (`GET /invoices`, `from`/`to`/`status`/`page`/`size`) and the sibling lists (`getPagopaList`, `getProformaInvoices`) to gather `fingerprint`s the tenant must pay.
2. **Create the bulk** — `createBulkPayment` (`POST /bulk`) with `documents`: a dictionary keyed by document type whose values are fingerprints, plus `allowWireTranfersAggregation`. Expect `201` with a NEW bulk `fingerprint`.
3. **Pay it once** — `createCheckout` (`POST /checkout`) with `kind` = bulk and that fingerprint; the payer completes one SCA at their bank. Fee rules (`GET /fee/rules/{kind}/{fingerprint}`) may add a fee document to the bulk automatically.
4. **Verify** — `getBulkPayment` (`GET /bulk/{fingerprint}`) and the per-document status; a checkout opened on a linked document after aggregation is redirected to the bulk automatically.

## Reversal
- `deleteBulkPayment` (`DELETE /bulk/{fingerprint}`) removes the aggregate only — "Deleting a bulk payment will not delete the linked documents". Once the transfer is executed there is no reversal; see `conventions/bancomat-conventions.yml`.

## Idempotency
- None; a repeated `createBulkPayment` creates another bulk document over the same fingerprints. Persist the returned fingerprint before any retry.

## Errors
- `400` when a fingerprint is not payable or not readable by the token; `403` on scope gaps; `429` at 100 req/min per IP. See `errors/bancomat-problem-types.yml`.
