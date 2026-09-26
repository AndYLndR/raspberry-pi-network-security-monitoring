# Firewall

## Objective

Restrict services to the minimum exposure required by the architecture without breaking Docker networking.

## Why the firewall was configured after Docker

Docker creates its own NAT and forwarding rules.

The firewall design was therefore finalized only after the real container networking and published ports were known.

## Custom chains

Two custom chains are used:

```text
RPI-HOST-IN
RPI-DOCKER-IN
```

The project does not edit Docker-managed rules directly.

## Host policy

Traffic arriving through `eth0` is restricted to the home LAN and required services.

Allowed services:

```text
22/tcp
53/tcp
53/udp
3000/tcp
3001/tcp
8080/tcp
20211/tcp
```

Everything else entering the host through Ethernet is dropped after the explicit allows.

## Restricted services

The following remain unavailable to normal LAN clients:

```text
9090/tcp  Prometheus
9100/tcp  Node Exporter
20212/tcp NetAlertX backend/API
```

## Persistence

Firewall rules are installed by:

```text
/usr/local/sbin/rpi-firewall.sh
```

and restored through:

```text
rpi-firewall.service
```

## Validation

From a Windows workstation:

```text
22/tcp    reachable
20211/tcp reachable
20212/tcp blocked
9100/tcp  blocked
```

Grafana and NetAlertX continued to function after these restrictions were applied.

## Evidence

```text
screenshots/security/firewall-status.png
```
