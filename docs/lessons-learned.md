# Lessons Learned

## 1. Validate before hardening

Security changes such as disabling SSH passwords should be applied only after the replacement access method has been tested.

## 2. Docker changes firewall behavior

Publishing a Docker port is not the same as opening a normal host service. Docker creates forwarding/NAT rules, so firewall design must account for Docker-managed chains.

## 3. Host networking should be justified

NetAlertX requires host networking for reliable Layer 2 discovery. This is a functional exception, not a default pattern for every container.

## 4. Observability is stronger when tools have distinct roles

Prometheus, Grafana and Uptime Kuma overlap conceptually, but they were assigned different responsibilities:

- Prometheus: metrics collection
- Grafana: metrics visualization
- Uptime Kuma: simple service availability

## 5. A dashboard is more valuable when its queries are understood

The Grafana dashboard was built manually using PromQL instead of importing a pre-built dashboard.

## 6. Backups are not useful unless they can be verified

The recovery archive was tested with `tar` and protected with a SHA256 manifest.

## 7. ISP routers can limit DNS deployment options

Some ISP-provided routers restrict custom DNS distribution.

A strong design should account for manual client DNS, Pi-hole DHCP, or a more capable router/firewall rather than assuming every router supports custom DHCP DNS.

## 8. Troubleshooting is part of the portfolio

The NetAlertX restart-loop problem became useful evidence of Docker permission, tmpfs and Linux-capability troubleshooting.
