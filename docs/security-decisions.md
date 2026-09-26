# Security Decisions

This project intentionally documents not only what was deployed, but why specific security choices were made.

## Raspberry Pi OS Lite

A headless Lite image was selected to reduce packages, background services and attack surface.

## Wired Ethernet

Ethernet is the primary interface. Wi-Fi remains unused for the server role.

## SSH keys before disabling passwords

Password authentication was not disabled until a separate ED25519 key-based login had been successfully validated.

This avoided creating a remote lockout scenario.

## Root SSH disabled

```text
PermitRootLogin no
```

The administrative user uses `sudo` for privileged actions.

## Unnecessary services disabled

The following services were disabled because they were not required by the server role:

- Avahi
- Bluetooth
- serial getty

## Docker user model

The administrative account was not added to the `docker` group.

Docker commands use `sudo` because membership in the `docker` group effectively grants root-equivalent control of the host.

## Docker log rotation

Docker was configured to use the `local` logging driver with bounded rotation.

This reduces the chance of container logs exhausting the 32 GB microSD.

## Prometheus kept internal

Prometheus does not need to be directly accessed by LAN clients.

Grafana reaches it through the Docker network using:

```text
http://prometheus:9090
```

## Node Exporter restricted

Node Exporter listens on the Raspberry Pi LAN address but is blocked from LAN clients by the host firewall.

Prometheus can still access it from the Docker bridge path.

## NetAlertX backend restricted

The NetAlertX Web UI remains available on port 20211.

The backend/API on 20212 is blocked from LAN clients.

## Firewall and Docker

Docker manages its own forwarding chains.

The project avoids editing Docker-managed chains directly. Host rules and Docker ingress filtering are kept in separate custom chains.

## Secrets

Real credentials are never committed to Git.

The repository includes `.env.example`, while `.env` remains private.

## Backups

Private application state and secrets are backed up separately from the public GitHub repository.
