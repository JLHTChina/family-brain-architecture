# Security and Permission Model

## 1. Permission levels

| Level | Examples | Policy |
|---|---|---|
| L0 Read-only | status, documents, inventory read | allowed by default, audited |
| L1 Reversible write | reports, uploads, notifications, jobs | automatic with audit and undo |
| L2 Irreversible | delete, send message, pay, network change | human approval, second confirmation, rollback plan |
| L3 Forbidden | root, company data, secret export, MFA bypass | never exposed to the model |

The model does not hold root, SSH, ADB, cloud credentials or MFA secrets. The tool runner holds credentials and enforces scopes.

## 2. Tool requirements

- JSON Schema with required fields and bounds.
- Parameter validation and allowlists.
- Timeouts, retries, idempotency keys.
- Audit log for every call and result.
- Dry-run/preview where possible.
- Rollback or compensation for writes.
- Kill switch and rate limits.
- Unregistered tools are unavailable.

## 3. Prompt injection

Untrusted content includes email, web pages, documents, images and transcripts. It must not become instructions.

- Separate the reader context from the actor context.
- Treat content as data, not instructions.
- Require explicit tool allowlists and human approval for side effects.
- Strip or quarantine suspicious instructions.
- Log the source of every tool call.

## 4. Data boundary

- No raw personal, school or company data in the public repository.
- Keep sensitive data local or in an approved tenant.
- Send derived events, transcripts and redacted crops before raw media.
- Encrypt in transit and at rest.
- Define retention and deletion.
- Do not mix personal, school and company tenants.

## 5. Human approval

- L2 actions always require a human.
- Approval is bound to a task capsule, not a blanket permission.
- The human sees the planned action, target, side effects and rollback.
- Approvals expire and are audited.
- No approval, no action; do not route around the policy.

## 6. Availability

- Core and memory should be on a UPS.
- Edge devices buffer during network loss.
- Single-session edges use explicit handoff.
- Fallback agents are leased, scoped and reconciled.
- A kill switch must stop outbound actions immediately.

## 7. Compliance

Implementations must add their own threat model, privacy review, consent model, data-processing agreements and applicable legal review. This document is not legal advice.
