# Publishing the Public Edition

This repository is a sanitized public edition. The private deployment and source of truth are not included.

## 1. Before publishing

- Confirm the public repository name and visibility.
- Confirm no secrets, credentials, private inventory, personal data, school data or company data.
- Run the secret scan and review the diff manually.
- Confirm licenses: Apache-2.0 for code, CC BY 4.0 for documentation.
- Confirm third-party notices and attribution.
- Use a fresh git history; do not publish private history.

## 2. Export process

1. Copy only allowlisted files from the private source.
2. Redact IPs, MACs, serials, order IDs, names, emails and internal paths.
3. Strip image metadata.
4. Review diagrams and screenshots.
5. Run `public_export.yaml` checks.
6. Commit with a sign-off.
7. Push to the public repository only after human approval.

## 3. Repository settings

- Enable branch protection for `main`.
- Require pull requests and status checks.
- Require signed-off commits.
- Restrict force pushes and deletions.
- Enable secret scanning and Dependabot alerts.
- Add a security policy and private vulnerability reporting.
- Add issue and PR templates.

## 4. Release checklist

- Update `CHANGELOG.md`.
- Update `CITATION.cff` version and date.
- Tag the release.
- Verify the public diff contains no private data.
- Publish release notes with scope and limitations.

## 5. Downstream changes

Public improvements may be cherry-picked back to the private source after review. Do not synchronize private history into the public repository.
