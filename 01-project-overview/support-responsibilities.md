# PayFlow Application & Product Support Responsibilities

**Document ID:** PF-SOP-001  
**Version:** 1.0  
**Purpose:** Define the simulated responsibilities of L1, L2 and Engineering/Ops.

## 1. Support operating principles

1. Own the ticket until it is resolved or explicitly accepted by the next team.
2. Verify the customer/merchant and record the affected resource before investigating.
3. Ask for references and timestamps, never passwords, PINs or one-time passcodes.
4. Use the least-privileged tool and access level necessary.
5. Preserve evidence before recommending a change.
6. Do not directly edit financial balances or delete financial records.
7. Communicate impact, next steps and update expectations in plain language.
8. Record investigation steps so another technician can continue without starting again.

## 2. L1 responsibilities

L1 is the first point of contact and handles intake, classification, known issues and approved first-line troubleshooting.

### Ticket intake
- Acknowledge the customer or merchant.
- Create a ticket and assign a unique ID.
- Capture issue summary, affected feature, timestamp, reference and impact.
- Verify identity using the approved demo procedure.
- Check whether the issue is already known or affects multiple users.

### First-line diagnosis
- Reproduce simple user-interface issues.
- Check account status and basic access conditions using approved views.
- Confirm transaction reference and displayed status.
- Check known service notices and knowledge base articles.
- Gather browser, device and error details where relevant.
- Perform only documented, reversible and authorized first-line actions.

### Customer communication
- Explain what is being checked.
- Avoid promising a resolution time unless a confirmed target exists.
- Provide a ticket reference.
- Give updates when the status changes or the agreed update interval is reached.

### L1 escalation triggers
Escalate when:
- A financial discrepancy or possible duplicate debit is reported.
- Multiple users are affected.
- A payment/order status mismatch cannot be explained.
- API or server errors persist after approved checks.
- Database, webhook, security or integration investigation is needed.
- The issue requires privileged access, code change or data correction.
- The incident meets the simulated P1/P2 criteria.

## 3. L2 responsibilities

L2 performs deeper technical investigation and coordinates with engineering or operations.

### Application investigation
- Reproduce the issue using a controlled test account.
- Inspect HTTP method, URL, status, request ID and safe request/response fields.
- Inspect Laravel logs and relevant exception context.
- Identify whether the issue is frontend, backend, database, integration or configuration related.
- Compare expected behaviour with actual behaviour.

### Database investigation
- Use read-only queries by default.
- Trace customer → wallet → transaction → ledger → payment/order relationships.
- Check transaction state, duplicate references, timestamps and related audit events.
- Validate balance calculations against ledger entries.
- Preserve query output and timestamps as evidence.
- Do not manually change balances or delete records.

### API and integration investigation
- Reproduce requests in Postman.
- Check authentication, headers, payload validation, response body and timing.
- Inspect webhook delivery, event identifiers, retry behaviour and idempotency.
- Separate provider-side failure from PayFlow application failure where evidence permits.

### Resolution and escalation
- Recommend a workaround only when safe and documented.
- Apply changes only in the local lab and within the stated authorization.
- Escalate code defects, infrastructure changes and privileged data operations to the appropriate owner.
- Verify the fix with a repeatable test.
- Document root cause, impact, evidence, resolution and prevention.

## 4. Engineering / Operations responsibilities

For this simulation, Engineering/Ops owns:
- Code changes and deployments.
- Database migrations and privileged data repair.
- Environment, server and network changes.
- Security incident response.
- Payment simulator defects beyond support configuration.
- Third-party integration code and infrastructure.

Support provides reproducible steps, impact, timestamps, references, logs and expected-versus-actual behaviour.

## 5. L1 vs L2 responsibility matrix

| Activity | L1 | L2 | Engineering/Ops |
|---|---|---|---|
| Ticket creation and classification | Own | Consult | — |
| Customer updates | Own | Support complex updates | As needed |
| Basic account checks | Own | Assist | — |
| Known workaround | Apply if approved | Validate | Approve where required |
| API request reproduction | Basic | Own complex cases | Assist |
| SQL investigation | Approved lookup only | Own read-only analysis | Privileged changes |
| Log analysis | Collect safe details | Own detailed analysis | Infrastructure/code-level |
| Root cause analysis | Contribute | Lead technical RCA | Lead code/infrastructure RCA |
| Production code change | No | No | Own |
| Financial data correction | No | Recommend/escalate | Authorized controlled process |
| Incident closure | Close after verification | Confirm technical resolution | Confirm change completion |

## 6. Simulated priority definitions

These are project exercise targets, not a claim about universal industry SLAs.

| Priority | Example impact | Initial response target | Handling |
|---|---|---:|---|
| P1 Critical | Widespread inability to use core payment functions or suspected broad financial integrity issue | 15 minutes | Immediate incident coordination and escalation |
| P2 High | Confirmed or suspected individual financial discrepancy, or major feature unavailable to a customer/merchant | 30 minutes | Prompt L2 investigation |
| P3 Medium | Limited feature issue with workaround available | 4 business hours | Normal queue and progress updates |
| P4 Low | General question or minor non-blocking issue | 1 business day | Standard support queue |

Response target means time to first meaningful response, not guaranteed time to resolution. The lab should record actual timestamps when later implemented.

## 7. Escalation handoff template

```text
Ticket ID:
Priority:
Customer/merchant identifier:
Affected feature:
Transaction/order/reference:
Date and time (include timezone):
Customer impact:
Steps to reproduce:
Expected result:
Actual result:
Troubleshooting already performed:
API status/request ID:
Relevant safe log excerpt:
Relevant read-only SQL findings:
Current workaround:
What is needed from L2/Engineering:
Customer update already sent:
```

## 8. Ticket closure checklist

- [ ] Customer/merchant impact is documented.
- [ ] Root cause is known or clearly marked as unconfirmed.
- [ ] Resolution or workaround is documented.
- [ ] Verification steps passed.
- [ ] Customer received a clear update.
- [ ] Relevant evidence is attached with secrets redacted.
- [ ] Follow-up or prevention action is recorded.
- [ ] Ticket status and resolution category are correct.

## 9. Example customer update

**Initial response**

“Thanks for reporting this. I understand that the payment is showing as completed on your side while the order still appears pending. I’ll check the payment reference and order status and update you once I have confirmed what happened. Please do not retry the payment until we have checked it, as this helps avoid a duplicate attempt.”

**Progress update**

“We have confirmed that the payment record is present, and we are checking why the order status has not updated. Your case is being investigated by our technical support team. We will share another update when the status has been verified.”

**Resolution update**

“We have verified that the order status now reflects the payment record. Please refresh the order page and confirm that it displays correctly. Your reference is [demo reference].”

Use only when the stated checks and outcome have actually occurred in the simulation.
