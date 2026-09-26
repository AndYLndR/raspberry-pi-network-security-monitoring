# Pi-hole

## Purpose

Pi-hole provides:

- DNS resolution
- DNS query visibility
- ad/tracker domain blocking
- centralized DNS security controls

## Container deployment

Pi-hole runs in Docker using a persistent named volume:

```text
pihole-data
```

## Published services

```text
192.168.1.36:53/tcp
192.168.1.36:53/udp
192.168.1.36:8080/tcp
```

## DHCP

Pi-hole DHCP was not enabled in the implemented configuration.

The home router remained the DHCP server.

## Secrets

The web password is supplied through a private `.env` file.

The public repository contains only:

```text
.env.example
```

## Validation

Normal DNS:

```bash
dig @192.168.1.36 example.com
```

returned `NOERROR`.

Blocked-domain validation:

```bash
dig @192.168.1.36 doubleclick.net
```

returned:

```text
0.0.0.0
EDE: 15 (Blocked)
```

## Pilot client

A Windows workstation was configured to use `192.168.1.36` as DNS and successfully browsed normally while Pi-hole recorded and filtered queries.

## LAN-wide deployment options

If the router supports custom DHCP DNS:

```text
DHCP clients -> 192.168.1.36 -> Pi-hole
```

If the ISP router does not support it:

- configure selected clients manually;
- use Pi-hole DHCP;
- use a more capable downstream router/firewall;
- request additional DHCP/DNS options from the ISP.

## Evidence

```text
screenshots/pihole/pihole-dashboard.png
```
