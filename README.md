# Bancomat (bancomat)
BANCOMAT S.p.A. is Italy's leading payment network operator managing the PagoBancomat debit card scheme, ATM network, and BANCOMAT Pay mobile payment service. Launched in 1983 for ATM withdrawals and expanded in 1986 with PagoBancomat for PIN-based POS payments, the network underpins Italian electronic payment infrastructure. BANCOMAT Pay, introduced in 2019, enables mobile e-commerce and P2P payments linked to bank accounts via phone number and IBAN.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/bancomat/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - ATM, Banking, Financial Services, Italy, Mobile Payments, Payments, Debit Cards

## Timestamps

- **Created:** 2024-01-15
- **Modified:** 2026-04-21

## APIs

### BANCOMAT Pay
BANCOMAT Pay is a mobile payment service enabling Italian consumers to make e-commerce purchases and P2P transfers through a smartphone app linked to their bank account by phone number and IBAN. Merchant integration is typically handled through PSPs such as Nexi, Axerve, PPRO, and HiPay rather than a direct public API.

**Human URL:** [https://bancomat.it/en/bancomat-pay](https://bancomat.it/en/bancomat-pay)

#### Tags:

 - Mobile Payments, P2P, Payments, Italy

#### Properties

- [Documentation](https://bancomat.it/en/bancomat-pay)
- [Nexi Integration Guide](https://developer.nexigroup.com/xpayglobal/en-EU/docs/bancomat-pay/)

## Common Properties

- [Website](https://bancomat.it/en)
- [About](https://bancomat.it/en/the-company)

## Features

| Name | Description |
|------|-------------|
| ATM Network | Italy's largest ATM cash withdrawal network operational since 1983. |
| PagoBancomat Debit | PIN-based POS debit card payments accepted at millions of Italian merchants. |
| BANCOMAT Pay Mobile | Mobile app payment service for e-commerce and P2P transfers linked to bank accounts. |
| QR Code Payments | QR code-based checkout integration for online and in-store merchants. |
| Bank Integration | Deep integration with Italian banks enabling account-linked payment authorization. |
| P2P Transfers | Person-to-person money transfers between Italian bank accounts via mobile app. |

## Use Cases

| Name | Description |
|------|-------------|
| ATM Cash Withdrawals | Debit card ATM withdrawals across Italy's national banking network. |
| POS Debit Payments | PIN-based debit card payments at retail point-of-sale terminals. |
| E-Commerce Payments | Online checkout integration via BANCOMAT Pay mobile app. |
| P2P Money Transfer | Person-to-person payments between bank accounts via mobile app. |
| Merchant Acceptance | Enable BANCOMAT Pay as a local Italian payment method for online stores. |

## Integrations

| Name | Description |
|------|-------------|
| Nexi | Integration via Nexi XPay Global payment gateway for merchant acceptance. |
| Axerve (Fabrick) | Integration via Axerve/Fabrick for Italian e-commerce BANCOMAT Pay acceptance. |
| PPRO | Integration via PPRO for international PSP access to BANCOMAT Pay. |
| HiPay | Integration via HiPay payment platform. |
| Viva.com | Integration via Viva.com payment services. |
| PayPal Braintree | Integration via PayPal Braintree payment gateway. |
| Nuvei | Integration via Nuvei payment technology platform. |

## Artifacts

Machine-readable API specifications organized by format.

### JSON-LD

- [BANCOMAT JSON-LD Context](json-ld/bancomat-context.jsonld)

## Capabilities

- [BANCOMAT Payment Capability](capabilities/bancomat-payment-capability.yaml) — Online checkout and P2P transfer workflows for Italian payment acceptance

## Vocabulary

- [BANCOMAT Vocabulary](vocabulary/bancomat-vocabulary.yaml) — Taxonomy covering 5 resources, 5 actions, 2 workflows, and 3 personas for Italian payment services

## Rules

- [BANCOMAT Spectral Rules](rules/bancomat-spectral-rules.yml) — 10 rules across 4 categories enforcing BANCOMAT API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
