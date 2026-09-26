# Services

## Service inventory

| Service | Role | Runtime |
|---|---|---|
| OpenSSH | Remote administration | Host |
| Node Exporter | Host metrics | Host |
| Firewall | Network access control | Host |
| Pi-hole | DNS filtering | Docker |
| NetAlertX | Device discovery | Docker / host networking |
| Uptime Kuma | Availability monitoring | Docker |
| Prometheus | Metrics collection | Docker |
| Grafana | Metrics visualization | Docker |

## Pi-hole

Provides:

- DNS resolution
- ad/tracker domain filtering
- DNS query visibility
- statistics

Pi-hole does not provide DHCP in the implemented configuration.

## NetAlertX

Provides:

- ARP-based discovery
- device inventory
- online/offline state
- new-device visibility

## Uptime Kuma

Provides simple service-health checks using Ping and HTTP.

## Prometheus

Scrapes Node Exporter every 15 seconds and stores the resulting time-series data.

## Grafana

Uses Prometheus as a datasource and provides the main system dashboard.

## Node Exporter

Exposes native host metrics including CPU, memory, filesystem, network, temperature and cooling-fan telemetry.
