# PayFlow Product Definition

**Document ID:** PF-PD-001  
**Version:** 1.0  
**Status:** Day 1 baseline  
**Product owner:** Portfolio project author  
**Last updated:** Day 1

## 1. Product summary

PayFlow is a fictional Nigerian digital wallet and merchant-payment application. It allows registered customers to view a wallet balance, initiate simulated wallet funding, transfer value between PayFlow wallets, review transaction history and pay participating demo merchants. Merchants can view simulated payments and track the payment status of demo orders.

PayFlow exists to provide a realistic but safe environment for demonstrating Level 1 and Level 2 Application Support and Product Support skills.

## 2. Problem statement

Users of financial applications may report problems such as failed login, balances that do not load, pending transactions, duplicate submissions, payment/order status mismatches or missing transaction records. Support specialists must be able to collect accurate details, identify the affected component, investigate using approved tools, communicate progress and escalate with useful evidence.

PayFlow provides controlled scenarios in which these support tasks can be practised and demonstrated.

## 3. Product vision

Provide a small, understandable fintech product whose behaviour and diagnostic evidence make it possible to demonstrate a complete support lifecycle: report → triage → investigate → resolve or escalate → verify → document.

## 4. Target users

### Customers
Individuals who have a PayFlow demo account and use a wallet to view balances, inspect transactions, make simulated transfers and pay demo merchants.

### Merchants
Demo businesses that receive PayFlow payments and need to inspect payment references and order/payment statuses.

### Support agents
Portfolio operator acting as L1 or L2 support. Agents use ticket records, customer-provided references, API responses, application logs and read-only database queries to investigate issues.

### Engineering / operations (simulated stakeholders)
The team to which support escalates defects, infrastructure problems, payment simulation faults or changes outside support authority.

## 5. Product value

- Gives customers a simple way to inspect simulated wallet activity.
- Gives merchants visibility into simulated payment outcomes.
- Gives support agents traceable references and reproducible diagnostic scenarios.
- Creates evidence of practical SQL, API, Laravel, incident-management and customer-communication skills.

## 6. Core capabilities

| Capability | Description | Support relevance |
|---|---|---|
| Authentication | Customer and merchant sign-in | Login, access and session issues |
| Wallet overview | Display wallet status and balance | Missing or stale balance |
| Simulated funding | Create a demo credit attempt | Pending/failed funding |
| Transfers | Transfer between demo wallets | Rejected, pending or duplicate request |
| Transaction history | Search by reference and date | Missing or incorrect records |
| Merchant payments | Associate a payment with an order | Payment/order mismatch |
| Merchant dashboard | View demo payment and order status | Merchant visibility and reporting |
| Diagnostic records | Correlation IDs, logs and audit events | L1/L2 investigation |

## 7. Key product principles

1. **No real money:** Every financial action is simulated.
2. **Traceability:** Each simulated financial operation has a unique reference.
3. **Consistency:** A transaction's status, ledger entries and displayed balance must be reconcilable.
4. **Idempotency:** Repeating the same operation with the same idempotency key must not create a second financial effect.
5. **Least privilege:** Support agents should use read-only access for investigation unless a documented, authorized operation is explicitly provided.
6. **Auditability:** Important state changes should record who/what performed the action and when.
7. **Safe communication:** Never ask customers to share passwords, PINs, one-time passcodes or full authentication tokens.
8. **Clear status:** Pending, successful, failed and reversed must have distinct meanings.

## 8. Transaction lifecycle

The initial model uses these statuses:

- `pending`: request accepted for processing; final outcome not yet confirmed.
- `successful`: simulated operation completed and corresponding ledger effect was recorded.
- `failed`: operation did not complete; no successful financial effect should be recorded.
- `reversed`: a previously successful operation was offset by a separately traceable reversal.

A reversal must not erase or overwrite the original transaction. It should be represented by a linked, auditable compensating entry.

## 9. Success criteria for the portfolio

The project is successful when the author can:

- Explain the product and its architecture.
- Demonstrate customer and merchant journeys.
- Locate a transaction using a reference.
- Use SQL to inspect related customer, wallet, transaction and ledger records.
- Use Postman to test documented API scenarios.
- Interpret relevant Laravel logs and HTTP responses.
- Produce a clear incident report and customer update.
- Distinguish an L1 resolution from an L2 investigation or engineering escalation.
- Demonstrate safe handling of synthetic financial data.

No claim of production uptime, real transaction volume, customer satisfaction improvement or business savings should be made.

## 10. Product glossary

| Term | Meaning |
|---|---|
| Wallet | Demo account balance container |
| Ledger | Append-only record of wallet credits and debits |
| Transaction reference | Unique identifier used to trace an operation |
| Payment | Simulated payment attempt associated with an order |
| Merchant | Demo business receiving a payment |
| Idempotency key | Client-supplied unique key used to prevent duplicate processing |
| Webhook | HTTP event notification sent by one system to another |
| Correlation ID | Identifier used to connect logs and events for one request |
| Reconciliation | Comparing related records to identify mismatches |
| RCA | Root cause analysis |
