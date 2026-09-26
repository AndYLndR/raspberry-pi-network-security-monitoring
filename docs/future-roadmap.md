# Future Roadmap

The project is intentionally complete at its current scope, but several extensions would make it more production-oriented.

## DNS resilience

Deploy a second independent Pi-hole or compatible resolver.

Goal:

```text
DNS resolver 1 -> Raspberry Pi A
DNS resolver 2 -> Raspberry Pi B
```

This removes the single-DNS dependency of a one-node design.

## Network-wide DHCP DNS distribution

Where the router supports it, advertise Pi-hole automatically through DHCP.

Alternative environments may use Pi-hole DHCP or a dedicated router/firewall.

## Alerting

Possible alert paths:

- new NetAlertX device
- Pi-hole unavailable
- disk usage threshold
- sustained high temperature
- monitoring target down
- backup failure

## Local DNS

Create friendly internal records for management services.

Examples:

```text
grafana.home
pihole.home
uptime.home
netalertx.home
```

## Storage

Migrate persistent data from microSD to SSD/NVMe.

## Backups

Automate scheduled backups to a separate device or storage location.

## Network segmentation

Extend visibility into separate VLANs for:

- trusted clients
- IoT
- servers
- lab devices

## HTTPS / reverse proxy

Introduce a local reverse proxy and trusted local certificates for management interfaces.

## SIEM integration

Potential future integration with the separate Home Cyber Range & Mini SOC Lab:

- syslog forwarding
- selected Pi-hole events
- NetAlertX events
- host logs
- correlation in Splunk
