---
generated: '2026-09-17'
method: generated
name: Issue an invoice and collect it through a hosted checkout
description: Create a FlowPay invoice document for a debtor, open a hosted checkout for it, hand the debtor the payment link, and confirm payment — with the only reversal paths that exist.
api: openapi/bancomat-flowpay-api-v2-openapi.yml
operations: [createInvoice, createCheckout, getCheckout, getPayments, deleteCheckout]
source: >-
  operationIds verified in openapi/bancomat-flowpay-api-v2-openapi.yml; lifecycle from
  github.com/FlowPay/client-openapi/docs/invoice_lifecycle.md; webhook events from
  asyncapi/bancomat-flowpay-webhooks.yml.
---

# Issue an invoice and collect it through a hosted checkout

FlowPay (a BANCOMAT company) models everything payable as a *document* identified by a content `fingerprint`; a *checkout* wraps one document into a hosted payment page where the debtor pays by PIS (bank transfer with SCA), SDD or card.

## Auth
- OAuth 2.0 bearer token from `https://core.flowpay.it/api/oauth/token` — `client_credentials` for your own tenant, `authorization_code` (+PKCE) when acting for another tenant. Scopes: `invoices:write`, then `invoices:read` / `payments:read`. See `authentication/bancomat-authentication.yml` and `scopes/bancomat-scopes.yml`.
- Base URL `https://api.flowpay.it/v2`. Rehearse in the sandbox first (`sandbox/bancomat-sandbox.yml`) — but payment-status webhooks do not fire there.

## Idempotency
- **None.** No `Idempotency-Key` header exists. A re-sent `createInvoice` with the same content is rejected as a duplicate document (v1 code 2012); a re-sent `createCheckout` creates a second checkout. Store the returned `fingerprint` and `code` before retrying anything. See `conventions/bancomat-conventions.yml`.

## Steps
1. **Create the invoice** — `createInvoice` (`POST /invoices`) with required `number`, `creditor`, `debtor` (VAT codes / codice fiscale), `terms[]` (amount + due date per instalment) and optional `items[]`, `attachments`. Expect `201`; keep `fingerprint`.
2. **Open the checkout** — `createCheckout` (`POST /checkout`) with required `kind` (`invoice`) and `fingerprint`, optional `okRedirectUrl` / `koRedirectUrl`, `locked`, `scaExempt`, `preferences`. Expect `201` with `code`, `collectionMethods[]` and, when the payer must authorise, a redirect link to the FlowPay payment page.
3. **Send the link** to the debtor (or generate many at once with the `fpy-generator` CLI — `cli/bancomat-cli.yml`).
4. **Confirm payment** — subscribe to `checkout_payment_authorized` / `checkout_payment_status_changed` (v1 webhooks; `asyncapi/bancomat-flowpay-webhooks.yml`, verify the ECDSA signature) or poll `getCheckout` (`GET /checkout/{code}`) and `getPayments` (`GET /payments`, filter by date window / status). Checkout UX events `checkout_opened` → `checkout_sca_opened` → `checkout_ok | checkout_ko` tell you where the payer stopped.

## Reversal
- Unpaid: `deleteCheckout` (`DELETE /checkout/{code}`) — "if the checkout has been paid, it cannot be deleted". v2 has no `deleteInvoice`.
- Paid: no refund/void endpoint. Issue `createCreditNote` (`POST /creditNotes`) linked to the original invoice, which "will automatically update the invoice status and amount due", and open a new checkout for the credit note if money must flow back.

## Errors
- `400` BadRequest carries `additionalInfo.path` naming the offending field; `401`/`403` are token/scope problems; `404` unknown fingerprint/code; `409` Conflict on state violations; `429` above 100 req/min per IP (no Retry-After). Quote `requestID` (live: `correlationId`) in tickets at https://youtrack.flowpay.it/. See `errors/bancomat-problem-types.yml`.
