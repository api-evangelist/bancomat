---
generated: '2026-09-17'
method: generated
name: Connect a tenant's bank account (AIS consent) and read balances
description: Start a PSD2 account-information consent session for a tenant, redirect the user to their bank, then read the linked accounts and transactions — and keep the 90-day consent alive.
api: openapi/bancomat-flowpay-api-v2-openapi.yml
operations: [getBanks, createAisConsentSession, getAccounts, getAccount, getTransactions]
source: >-
  operationIds verified in openapi/bancomat-flowpay-api-v2-openapi.yml; consent semantics from
  github.com/FlowPay/client-openapi/docs/general.md (AIS section) and the v1 contract
  (consent_expiring / consent_expired webhooks); OIDC metadata at
  well-known/bancomat-flowpay-openid-configuration.json.
---

# Connect a tenant's bank account (AIS consent) and read balances

FlowPay is a Bank of Italy-authorised AISP: it collects the PSD2 consent with the user's bank so your client never implements a bank-by-bank consent flow.

## Auth
- Token with `accounts:write` for the consent session, `accounts:read` to read. In v1 the same flow starts with a `client_credentials` token carrying scope `authorization_intent` that creates a consent, which the user then authorises through the `authorization_code` flow with a signed request object (see `authentication/bancomat-authentication.yml`, `details.consent_model`).
- Public sandbox: two fake businesses with fake accounts and fake AIS data; real banks return no balances there.

## Steps
1. **List banks** — `getBanks` (`GET /banks`, optional `country`); this endpoint answered unauthenticated on 2026-09-17. Keep the bank `id`.
2. **Start the consent session** — `createAisConsentSession` (`POST /accounts`) with required `tenantID` and the chosen `bank`. Expect `201 { link }`.
3. **Redirect the user** to `link`; the bank performs SCA and the consent lands in FlowPay. The v2 contract's `AISConsentStatus` webhook (status `ACTIVATED` | `REVOKED` | `EXPIRED`) or, in v1, `consent_expiring` (~7 days before) / `consent_expired` events report the consent state.
4. **Read accounts** — `getAccounts` (`GET /accounts`, params `page`, `tenantID`, `bank`, `consent`), then `getAccount` (`GET /accounts/{accountID}`) for detail and `getTransactions` (`GET /transactions`, `accountID`, `from`, `to`, `page`, `size`) for history. v1 exposes balances at `GET /{tenantID}/balances` and `/balances/last`.

## Consent lifetime
- Recurring AIS consents expire **90 days after creation** (v1 contract, `consent_expired`); the user can also revoke at the bank at any time and most banks send no `rejectionReason`. Re-run step 2 to renew — there is no silent renewal.

## Idempotency / reversal
- No idempotency header; a repeated `createAisConsentSession` simply opens another session. There is no API to revoke a consent — revocation happens at the bank or via the FlowPay account portal.

## Errors
- `401`/`403` on missing `accounts:*` scope; `404` unknown account; `429` at 100 req/min per IP. See `errors/bancomat-problem-types.yml`.
