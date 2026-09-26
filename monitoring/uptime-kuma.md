# Uptime Kuma

## Purpose

Uptime Kuma provides a simple availability view for important infrastructure components.

## Runtime

Docker container with persistent application state.

Named volume:

```text
uptime-kuma-data
```

## Initial monitors

| Friendly name | Type | Target |
|---|---|---|
| Raspberry Pi | Ping | `192.168.1.36` |
| Home Router | Ping | `192.168.1.1` |
| Pi-hole Web | HTTP(s) | `http://192.168.1.36:8080/admin/` |
| NetAlertX | HTTP(s) | `http://192.168.1.36:20211` |

## Why use Uptime Kuma when Prometheus exists?

The roles are intentionally different:

- Prometheus collects metrics.
- Grafana visualizes metrics.
- Uptime Kuma provides a simple operational answer to: **is this service reachable right now?**

## Evidence

```text
screenshots/uptime-kuma/service-monitoring-dashboard.png
```
