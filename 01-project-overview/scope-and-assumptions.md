# PayFlow Scope, Assumptions and Risks

**Document ID:** PF-SCOPE-001  
**Version:** 1.0

## 1. In scope

- Local Laravel application on Windows/XAMPP.
- MySQL database with synthetic customers, wallets, merchants and transactions.
- Customer and merchant demo journeys.
- Simulated wallet funding, transfers and merchant payments.
- REST API endpoints for the demo functions.
- Application logging and request correlation.
- Support-focused SQL and API investigation.
- Incident reports, runbooks and knowledge base.
- Optional n8n workflow demonstration using test events.

## 2. Out of scope

- Real financial services or movement of funds.
- Live bank, card or payment-provider integrations.
- Real KYC, identity verification or regulatory compliance.
- Production hosting or real customer data.
- Publicly accessible admin or support console.
- Unreviewed automated balance correction.
- Storing or processing real payment credentials.

## 3. Technical assumptions

- Windows PC with XAMPP installed.
- MySQL service is available and a local database can be created.
- Composer is installed and available in the terminal.
- A Laravel version compatible with the installed PHP version will be selected after checking the environment.
- Git is installed.
- Postman can be used for API testing.
- The application will run locally during the initial build.
- `.env` will contain local configuration and will not be committed.

## 4. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Laravel/PHP version mismatch | Check `php -v`, Composer and Laravel compatibility before project creation |
| Existing XAMPP/MariaDB instability | Back up important local databases before making configuration changes |
| Accidental use of real data | Use generated `.test` emails and synthetic references only |
| Exposed secrets in Git | Keep `.env` out of Git; commit `.env.example` only |
| Incorrect wallet logic | Use database transactions, ledger entries and idempotency |
| Misleading portfolio claims | Label every scenario as simulated and record actual evidence |
| Scope too large for 14 days | Prioritize support evidence over feature completeness |
| Unsafe support remediation | Read-only investigation by default; document authorization for changes |

## 5. Definition of done

Day 1 is complete when:
- Product purpose and users are documented.
- Functional and non-functional requirements are defined.
- Customer and merchant journeys are documented.
- L1/L2 responsibilities and escalation rules are defined.
- Initial repository structure exists.
- The next implementation steps are clear.
