# System Hardening

## Updates

The system was fully updated before application deployment.

Automatic Debian updates were enabled with `unattended-upgrades`.

The configuration enables:

```text
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

Raspberry Pi repository packages remain part of normal maintenance rather than being misrepresented as automatically covered by the Debian unattended-upgrade policy.

## Services disabled

The following services were disabled because they were unnecessary for the server role:

- Avahi / mDNS
- Bluetooth
- serial getty

## Logging

Persistent systemd journal storage was present under:

```text
/var/log/journal
```

## AppArmor

AppArmor packages were present, but AppArmor was not active as an LSM in the running system.

The project did not modify boot/kernel parameters solely to claim AppArmor hardening.

## Docker logging

Docker uses bounded local log rotation to protect microSD capacity.

## Administrative model

- non-root administration
- `sudo` for privileged actions
- no Docker group membership
- SSH key authentication
