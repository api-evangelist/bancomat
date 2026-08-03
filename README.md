# Bancomat (bancomat)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
