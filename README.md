# PayFlow — Fintech Application Support & Incident Management Lab

**Project type:** Independent portfolio project  
**Domain:** Fintech / digital wallet / payment operations  
**Support scope:** Level 1 and Level 2 Application & Product Support  
**Stack:** PHP, Laravel, MySQL, XAMPP, REST APIs, Postman, n8n  
**Status:** Day 1 — Product definition and requirements

> **Safety notice:** PayFlow is a fictional training environment. All users, merchants, balances, transaction references and incidents are synthetic. It does not process real money or connect to a live payment provider.

## Project purpose

PayFlow is a deliberately small digital wallet and merchant-payment application used to demonstrate practical application support work. The portfolio focuses on diagnosing user-reported issues, collecting evidence, investigating API/database/application behaviour, communicating clearly, documenting incidents and escalating issues safely.

This is a support portfolio first, not a production fintech product.

## Day 1 scope

- Product definition and boundaries
- Product requirements
- Customer and merchant journeys
- L1/L2 support responsibilities
- Initial repository structure

## Planned product capabilities

1. Customer registration and authentication
2. Customer wallet and balance display
3. Simulated wallet funding
4. Simulated wallet-to-wallet transfer
5. Transaction history and transaction lookup
6. Merchant payment and order status
7. Merchant transaction view
8. Support-oriented audit and diagnostic evidence

## Support scenarios to demonstrate

- Login and account access failures
- Wallet balance not loading
- Pending or failed simulated funding
- Transfer rejected or pending
- Duplicate transaction submission
- Payment completed but merchant order remains pending
- API authentication and validation errors
- Database connection and query failures
- Webhook delivery and duplicate-event handling
- Incorrect dashboard totals

## Repository map

```text
payflow-application-support/
├── README.md
├── 01-project-overview/
│   ├── product-definition.md
│   ├── product-requirements.md
│   ├── customer-journey.md
│   ├── merchant-journey.md
│   ├── support-responsibilities.md
│   └── scope-and-assumptions.md
├── 02-architecture/
│   └── day1-logical-architecture.md
├── 03-planning/
│   └── 14-day-build-plan.md
└── 04-evidence/
    └── evidence-register.md
```

## How to use this repository

1. Read `01-project-overview/product-definition.md`.
2. Review the requirements and journeys.
3. Use the architecture note to guide the Laravel implementation.
4. During later days, add database schema, API documentation, Postman collections, incident reports, runbooks and screenshots.
5. Only mark an item complete when you have implemented or tested it and captured evidence.

## Portfolio integrity

Clearly label simulated incidents and test data. Do not claim that this lab represents production payment operations or real customer outcomes. Never publish credentials, API tokens, private customer information or production data.

## Target outcome

A recruiter should be able to follow a customer complaint from initial ticket through triage, investigation, root-cause hypothesis, approved resolution, verification, customer update and closure.
