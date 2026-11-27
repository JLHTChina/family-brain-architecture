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

## 8. Sole ownership and delegated authority

- The human owner is the sole authority. The AI is never an owner, collaborator, organization admin, recovery principal or billing contact.
- The AI receives scoped, revocable capabilities, not account ownership or standing credentials.
- No shared accounts, shared passwords or shared MFA devices.
- Automation that needs write access uses a least-privilege, repository-scoped deploy key or fine-grained token; no admin scope; no access to other repositories.
- The owner reviews and merges changes. A bot may open a pull request, but it does not approve or merge its own change.
- Recovery paths (hardware key, recovery codes, break-glass procedure) are held by the owner, offline and separate from the automation.

## 9. Encryption and key hierarchy

| Secret | Storage | Rule |
|---|---|---|
| Account 2FA | hardware security key/passkey + TOTP backup | never shared; recovery codes offline |
| SSH key | local OS keychain/agent, passphrase-protected | public key only on GitHub; private key never in repo |
| Commit signing key | SSH signing or GPG, passphrase-protected | public key on GitHub; verify before release |
| Personal access token | secrets manager; fine-grained, expiring | no classic PAT; no repo commit; least privilege |
| Service secrets | OS keychain/DPAPI, age/SOPS or secret manager | never in prompts, logs, screenshots or public repo |
| Sensitive backups | encrypted container (age/VeraCrypt) | key stored separately; restore tested |

- Encrypt in transit (HTTPS/SSH) and at rest (full-disk encryption on owner devices).
- Do not store private keys, recovery codes or tokens in this public repository, issues, pull requests or CI logs.
- Rotate tokens and keys on a schedule and immediately after suspected exposure.
- Prefer short-lived credentials and OIDC over long-lived cloud keys.

## 10. Threat model

- Account takeover: phishing, password reuse, stolen session, SIM swap.
- Supply chain: unpinned GitHub Actions, malicious dependencies, compromised maintainer.
- Secret leakage: committed `.env`, logs, screenshots, issue attachments.
- Malicious contribution: prompt injection in a PR, workflow injection, untrusted code execution.
- Repository integrity: force push, branch deletion, tag rewriting.
- Automation abuse: over-scoped token, prompt injection causing tool misuse.

## 11. Incident response

1. Revoke sessions, tokens, deploy keys and app authorizations.
2. Rotate affected keys and secrets.
3. Preserve audit logs and evidence.
4. Inspect commits, releases, workflows and public exposure.
5. Notify affected parties if personal data was exposed.
6. Restore from a verified backup; verify signatures and checksums.
7. Record the incident and update the threat model.

See [github-hardening.md](github-hardening.md) for the concrete GitHub settings checklist.

