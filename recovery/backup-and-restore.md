# Backup and Restore

## Strategy

The recovery model separates:

1. public/reproducible configuration;
2. private secrets;
3. persistent application state;
4. host configuration.

## Persistent Docker volumes

```text
grafana-data
netalertx-data
pihole-data
prometheus-data
uptime-kuma-data
```

## Consistent volume backup

Application containers were stopped before volume archives were created to reduce the risk of copying database files during active writes.

Each named volume was exported to a compressed tar archive using a temporary Alpine container.

## Validation

Each archive was tested using:

```bash
tar -tzf <archive>.tar.gz
```

A SHA256 manifest was generated for integrity verification.

## Complete recovery package

The private recovery package includes:

```text
repo/
host-config/
volumes/
secrets/
manifest/
RESTORE-NOTES.md
```

The private archive is **not** intended for GitHub.

## Restore order

1. Install Raspberry Pi OS Lite 64-bit.
2. Configure hostname and LAN addressing.
3. Install Docker Engine and Compose.
4. Restore host configuration.
5. Restore Docker named volumes.
6. Restore repository files.
7. Restore the private `.env`.
8. reload systemd.
9. start Docker services.
10. validate DNS, dashboards, monitoring and firewall behavior.

## Example volume restore pattern

Conceptually:

```bash
sudo docker volume create <volume-name>

sudo docker run --rm \
  -v <volume-name>:/restore \
  -v /path/to/backups:/backup:ro \
  alpine \
  sh -c 'cd /restore && tar -xzf /backup/<archive>.tar.gz'
```

Containers should remain stopped while restoring their application data.

## Important

A backup stored only on the same microSD does not protect against physical card failure.

At least one copy should be kept off the Raspberry Pi.
