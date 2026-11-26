# PayFlow Product Requirements Document (PRD)

**Document ID:** PF-PRD-001  
**Version:** 1.0  
**Status:** Baseline requirements for portfolio implementation

## 1. Objective

Define the minimum functional and non-functional requirements for a simulated fintech application that supports practical L1/L2 troubleshooting exercises.

## 2. User roles

| Role | Permissions |
|---|---|
| Customer | View own profile, wallet, transactions and initiate permitted demo actions |
| Merchant | View own merchant profile, demo orders and associated payments |
| Support L1 | View support tickets and approved customer/transaction details; perform documented first-line checks |
| Support L2 | Perform deeper read-only diagnostics across API, logs and related records; recommend or perform authorized non-production remediation |
| Administrator | Manage demo configuration and test users; not used for routine support investigations |

Role checks must be enforced on the server, not only hidden in the user interface.

## 3. Functional requirements

### FR-01: Authentication
- Customers and merchants can sign in with valid credentials.
- Invalid credentials return a safe error without revealing whether an email address exists.
- Protected routes require authentication.
- Logout invalidates the active session/token.
- Passwords are stored using Laravel's supported password hashing.

**Acceptance criteria:** Valid demo user can sign in; invalid credentials are rejected; unauthenticated requests to protected endpoints return HTTP 401.

### FR-02: Customer wallet overview
- An authenticated customer can view their own wallet.
- The response includes wallet identifier, status, currency and displayed balance.
- A customer cannot view another customer's wallet by changing an ID.

**Acceptance criteria:** Own wallet is returned; unauthorized cross-customer access is denied; a missing wallet produces a controlled response.

### FR-03: Simulated wallet funding
- A customer can submit a simulated funding request.
- Each request receives a unique transaction reference.
- The simulator can produce configured outcomes such as successful, pending or failed.
- A successful credit must have a corresponding ledger entry.
- Repeating a request with the same idempotency key must not create a second credit.

**Acceptance criteria:** Every request has a traceable result; duplicate idempotency key does not create a duplicate financial effect; failed/pending attempts do not silently increase available balance.

### FR-04: Simulated wallet transfer
- An authenticated customer can transfer a permitted amount to another active demo wallet.
- The system validates sender, recipient, amount and available balance.
- A transfer must be traceable using one reference.
- The sender debit and recipient credit must be atomic: both succeed or neither financial effect is committed.
- Duplicate submissions are protected by idempotency.

**Acceptance criteria:** Valid transfer updates both ledger positions consistently; insufficient balance is rejected; invalid recipient is rejected; duplicate request does not transfer twice.

### FR-05: Transaction history
- Customers can view only their own transaction history.
- Results are ordered newest first and support pagination.
- A transaction can be searched by reference.
- Sensitive internal fields are not exposed.

**Acceptance criteria:** Correct records are returned for the authenticated customer; unknown references return a controlled not-found response.

### FR-06: Merchant orders and payments
- A merchant can view only its own demo orders.
- A demo order can be associated with a simulated payment.
- Payment and order statuses are stored separately.
- A successful payment event updates the associated order through a controlled application process.
- Duplicate payment events do not duplicate the order's paid effect.

**Acceptance criteria:** Merchant sees its own order and payment state; another merchant's records are inaccessible; repeated event processing is idempotent.

### FR-07: Support diagnostic traceability
- Requests should have a correlation/request ID.
- Application logs should record relevant technical events without passwords, tokens, PINs or full payment credentials.
- Transaction references should appear in appropriate diagnostic records.
- Support investigation should be possible without direct production-style data modification.

**Acceptance criteria:** A support investigator can correlate a test request with relevant logs using a request ID or transaction reference.

### FR-08: Error handling
- Validation errors use a consistent response format.
- Authentication failures return HTTP 401.
- Authorization failures return HTTP 403.
- Missing resources return HTTP 404.
- Unexpected server errors return a generic message and a traceable reference; stack traces are not shown to end users.

**Acceptance criteria:** Error responses are predictable and do not disclose secrets or internal stack traces.

## 4. Non-functional requirements

| ID | Requirement |
|---|---|
| NFR-01 | Application runs locally on Windows using XAMPP-supported PHP and MySQL, with a compatible Laravel version |
| NFR-02 | Financial changes use database transactions |
| NFR-03 | Financial records are traceable and not silently overwritten |
| NFR-04 | Passwords are hashed; secrets are kept in environment configuration |
| NFR-05 | Role and ownership authorization is enforced server-side |
| NFR-06 | Logs exclude passwords, PINs, access tokens and other secrets |
| NFR-07 | API responses use consistent JSON structures |
| NFR-08 | Demo data is synthetic and clearly identified |
| NFR-09 | Database queries used by support are read-only unless an authorized test remediation is documented |
| NFR-10 | The application is usable on a typical desktop browser; responsive layout is desirable |

## 5. Out of scope

- Real deposits, withdrawals, bank transfers or card processing.
- Connection to live banks, payment gateways or financial institutions.
- Real customer identity verification or KYC.
- Real money, stored value or financial advice.
- Production deployment or production-grade security certification.
- Mobile applications.
- Automated support ticket integration in the first application milestone.
- Regulatory compliance claims.

## 6. Key business rules

1. Currency is NGN for all demo wallets and transactions.
2. Amounts must be greater than zero and use two decimal places.
3. A wallet must be active to perform a financial operation.
4. A transfer cannot be sent to the same wallet.
5. A customer can access only records they own.
6. A merchant can access only its own orders and payments.
7. Transaction references are unique.
8. Ledger entries are append-only for normal application operations.
9. Reversals are new compensating entries linked to the original transaction.
10. A pending operation must not be represented as successful.
11. Duplicate requests must not produce duplicate financial effects.
12. All timestamps are stored consistently; display timezone is documented by the application.

## 7. Initial API response convention

Successful response example:

```json
{
  "success": true,
  "message": "Wallet retrieved successfully.",
  "data": {
    "wallet_id": 12,
    "currency": "NGN",
    "balance": "25000.00",
    "status": "active"
  },
  "request_id": "req_demo_001"
}
```

Validation error example:

```json
{
  "success": false,
  "message": "The submitted data is invalid.",
  "errors": {
    "amount": ["The amount must be greater than zero."]
  },
  "request_id": "req_demo_002"
}
```

Unexpected error example:

```json
{
  "success": false,
  "message": "We could not complete your request. Please try again later.",
  "request_id": "req_demo_003"
}
```

## 8. Acceptance and test approach

Each functional requirement will have:
- At least one successful-path test.
- At least one validation or failure-path test.
- An authorization test where data ownership is relevant.
- Evidence such as Postman output, SQL results, screenshots or logs.

Financial operations additionally require duplicate-request and ledger-consistency tests.
