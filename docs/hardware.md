# Hardware

## Raspberry Pi

| Item | Value |
|---|---|
| Model | Raspberry Pi 5 |
| RAM | 4 GB |
| Architecture | ARM64 / aarch64 |
| Cooling | Raspberry Pi Active Cooler |
| Storage | SanDisk 32 GB microSD |
| Network | Gigabit Ethernet |

## Why this hardware?

The workload is lightweight enough that a Raspberry Pi 5 with 4 GB RAM is sufficient for:

- Pi-hole
- NetAlertX
- Uptime Kuma
- Prometheus
- Grafana
- Node Exporter

The Active Cooler provides controlled thermal behavior for continuous operation.

## Storage decision

A 32 GB microSD was used for the project because it was already available and provided enough capacity for the initial scope.

To reduce unnecessary storage growth:

- Docker logging uses the `local` logging driver;
- Prometheus retention is limited;
- persistent data uses named volumes;
- backups are exported off-device.

## Future hardware improvement

For long-term 24/7 use, SSD or NVMe storage would be preferred over microSD because monitoring workloads generate continuous writes.
