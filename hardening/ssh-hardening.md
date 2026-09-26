# SSH Hardening

## Objective

Provide remote administration without relying on account passwords.

## Key generation

An ED25519 key pair was generated on the administrator workstation.

The private key remains on the workstation.

## Server-side key installation

The public key was added to:

```text
~/.ssh/authorized_keys
```

Permissions:

```text
~/.ssh               700
~/.ssh/authorized_keys 600
```

## Effective hardened configuration

```text
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
```

The configuration was validated with:

```bash
sudo sshd -t
sudo sshd -T
```

## Safe change sequence

1. Keep the current SSH session open.
2. Create a second connection using the new key.
3. Verify key authentication works.
4. Disable password and keyboard-interactive authentication.
5. Reload SSH.
6. Test a fresh connection again.

## Validation

A forced password-only connection failed as expected.

## Evidence

```text
screenshots/security/ssh-hardening.png
```
