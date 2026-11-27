# GitHub Hardening Checklist

This checklist is for the owner of the public repository. It is intentionally conservative: the human owner is the sole authority; automation gets scoped, revocable capabilities only.

## 0. Scope: GitHub only

These steps are scoped to the GitHub account and this repository. They do **not** change:

- Windows/macOS login, Windows Hello, or device passwords;
- VPN, proxy, DNS, hosts file, or network routes;
- router, AP, NAS, PC firewall, or UPS;
- global Git configuration (`git config --global`);
- other repositories or other accounts.

VPN coexistence:

- GitHub 2FA/passkey works over a VPN; it does not require changing the VPN.
- If the VPN changes your apparent location, GitHub may ask for an extra verification; use email/TOTP/recovery, do not bypass it.
- If SSH port 22 is blocked by the VPN or network, use GitHub's SSH-over-443 endpoint (`ssh.github.com:443`) in `~/.ssh/config`; do not change the VPN.
- If Git over SSH is blocked entirely, use HTTPS with a credential manager or a fine-grained token for this repository only.

Commit signing:

- Configure signing with `git config --local`, inside this repository only.
- Do not use `git config --global`; other repositories keep their current behavior.
- If signing fails, it affects only this repository; disable it locally and fix before pushing.

Do not lock yourself out:

- Enable 2FA while your current session is active.
- Save recovery codes offline before finishing.
- Keep a TOTP backup in addition to a hardware key/passkey.
- Test in a private browser window before signing out other devices.
- Do not remove the existing SSH key until the new key has been tested.


## 1. Account

- [ ] Personal account; no shared login.
- [ ] 2FA enabled with a hardware security key or passkey as primary; TOTP as backup.
- [ ] Recovery codes printed/stored offline in two separate places.
- [ ] No SMS-only 2FA.
- [ ] Real, long-term email; email account also protected by 2FA.
- [ ] "Keep my email addresses private" enabled; commits use `@users.noreply.github.com`.
- [ ] Review active sessions and authorized OAuth apps; revoke unknown ones.
- [ ] No collaborators, no organization admin, no billing delegation.
- [ ] AI/bots are not owners, admins or recovery principals.

## 2. Repository ruleset for `main`

- [ ] Require a pull request before merging.
- [ ] Require status checks to pass.
- [ ] Require signed commits.
- [ ] Require linear history.
- [ ] Block force pushes.
- [ ] Block branch deletion.
- [ ] Restrict who can push (owner only; no bots with direct write).
- [ ] Do not require a second-person approval on a solo project; use owner merge with status checks.
- [ ] CODEOWNERS points to the owner.

## 3. Secrets and supply chain

- [ ] Secret scanning and push protection enabled.
- [ ] Dependabot alerts and security updates enabled.
- [ ] Actions permissions default to read-only.
- [ ] Pin third-party Actions to commit SHAs; use Dependabot to update them.
- [ ] Do not use `pull_request_target` with untrusted code.
- [ ] No secrets in workflow logs; mask sensitive values.
- [ ] Environment protection for any deployment secrets.
- [ ] No long-lived cloud keys; prefer OIDC.
- [ ] Review workflow changes like code changes.

## 4. Keys and signing

- [ ] SSH key: ed25519, passphrase-protected, one key per device.
- [ ] Commit signing: SSH signing or GPG; verify with `git log --show-signature`.
- [ ] Public keys only in GitHub; private keys never in the repository.
- [ ] Fine-grained PAT with an expiry and only the required repository/scope.
- [ ] No classic PAT with broad `repo`/`admin` scopes.
- [ ] Rotate keys/tokens on a schedule and after any suspected exposure.

## 5. Public data boundary

- [ ] No secrets, tokens, private keys or `.env` files.
- [ ] No personal data, school data, company data or private inventory.
- [ ] No real hostnames, IPs, MAC addresses, serial numbers or order IDs.
- [ ] Images stripped of EXIF/GPS metadata.
- [ ] Third-party licenses and notices checked.
- [ ] Public export reviewed manually before push.

## 6. Operations

- [ ] Private vulnerability reporting enabled.
- [ ] Security policy published.
- [ ] Audit log reviewed periodically.
- [ ] Backup of the private source of truth is encrypted and restore-tested.
- [ ] Incident response steps are documented and reachable offline.
