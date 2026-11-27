# Security Policy

## Scope

This repository is a public architecture reference. It does not contain a deployed service, credentials or private data. Security reports should concern the architecture, patterns or example code in this repository.

## Reporting

Please report vulnerabilities privately through GitHub Security Advisories or the repository owner's published security contact. Do not open a public issue with exploit details, secrets or personal data.

Include:

- affected file or pattern;
- impact and preconditions;
- reproduction steps with synthetic data only;
- suggested mitigation, if known.

## Security principles

- Read-only by default; writes reversible by default; irreversible actions require human approval.
- The owner is the sole authority; the AI is never an owner, admin or recovery principal.
- The model does not hold root, SSH, ADB, cloud credentials or MFA secrets.
- Tools are registered, schema-validated, allowlisted and audited.
- Untrusted content is separated from the instruction context to reduce prompt injection.
- No raw personal data, school data, company data or secrets in this repository.
- No public RDP, no open inbound ports, no MFA bypass.
- Kill switch and audit trail are mandatory for any implementation.

See [docs/github-hardening.md](docs/github-hardening.md) for the concrete account, repository, signing and Actions checklist.

## Supported versions

This is a living architecture document. Security fixes are applied to the current public edition; older snapshots may not be supported.
