# NetAlertX

## Purpose

NetAlertX provides:

- device discovery
- asset inventory
- online/offline state
- vendor information
- visibility of newly discovered devices

## Network mode

NetAlertX uses:

```yaml
network_mode: host
```

This is required for reliable ARP-based Layer 2 discovery.

## Scan scope

```text
192.168.1.0/24 --interface=eth0
```

A Docker `/16` network was intentionally excluded from the scan scope to avoid unnecessary scanning and plugin timeouts.

## Security model

The container uses a read-only filesystem and drops all capabilities before selectively restoring only the capabilities needed by the application.

Configured capabilities:

```text
NET_ADMIN
NET_RAW
NET_BIND_SERVICE
CHOWN
SETUID
SETGID
```

## Ports

```text
20211/tcp  Web UI
20212/tcp  backend/API
```

The Web UI is reachable from the LAN.

The backend/API is blocked from LAN clients by the host firewall.

## Troubleshooting

The initial container entered a restart loop because tmpfs permissions did not match the application's startup requirements.

See:

```text
troubleshooting/README.md
```

## Evidence

```text
screenshots/netalertx/network-device-inventory.png
```
