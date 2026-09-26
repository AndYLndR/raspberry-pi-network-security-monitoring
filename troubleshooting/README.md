# Troubleshooting

## NetAlertX restart loop

### Symptoms

After the initial deployment:

```text
netalertx -> Restarting (1)
```

The logs contained errors similar to:

```text
mkdir: can't create directory '/tmp/log': Permission denied
mkdir: can't create directory '/tmp/run': Permission denied
tee: /tmp/log/app.php_errors.log: Permission denied
Service nginx exited with status 1.
```

### Root cause

The container used:

- a read-only root filesystem;
- a tmpfs mount for `/tmp`;
- dropped Linux capabilities.

The initial tmpfs/capability combination prevented the startup process from creating and changing ownership of required runtime directories.

### Resolution

The container was kept hardened rather than switching to `privileged: true`.

The fix included:

```text
CHOWN
SETUID
SETGID
```

in addition to the networking capabilities required by NetAlertX:

```text
NET_ADMIN
NET_RAW
NET_BIND_SERVICE
```

The `/tmp` tmpfs ownership and mount options were also aligned with the application's expected runtime UID/GID.

### Result

After recreation:

```text
running healthy
```

NetAlertX successfully performed ARP discovery of the local `/24` network.

---

## DNS login/configuration issue

### Symptom

The Pi-hole web interface rejected the expected password.

### Investigation

The environment variable was confirmed inside the container without printing its real value.

### Resolution

The `.env` value was updated using a password without characters that could be unexpectedly interpreted by Compose, and the Pi-hole container was recreated.

### Result

The web UI accepted the configured credential and the secret remained outside the repository.

---

## `resolvectl` not found

### Symptom

```text
-bash: resolvectl: command not found
```

### Resolution

No additional resolver stack was installed just to obtain the command.

NetworkManager tools were used instead:

```bash
nmcli connection show --active
nmcli device show eth0
cat /etc/resolv.conf
```

---

## Docker + firewall exposure

### Observation

Docker-published ports initially appeared on:

```text
0.0.0.0
[::]
```

### Resolution

LAN-facing Docker services were rebound explicitly to:

```text
192.168.1.36
```

Prometheus publishing was removed entirely because Grafana could access it over the internal Docker network.

Node Exporter and the NetAlertX backend were filtered at the host firewall.

---

## Validation principle

No issue was documented as fixed until the service was re-tested after the change.
