# Network Configuration

## Baseline

```text
Interface: eth0
Address:   192.168.1.36/24
Gateway:   192.168.1.1
Network:   192.168.1.0/24
```

The initial address was assigned through DHCP.

## Stable addressing

A router-side DHCP reservation was created for the Raspberry Pi.

This approach was preferred over manually forcing a static address on the host because the router remains the source of truth for address assignment.

## DNS before Pi-hole client testing

Before client testing, the Raspberry Pi itself received DNS through the router.

## Pi-hole pilot client

A Windows workstation was configured manually to use:

```text
192.168.1.36
```

as its IPv4 DNS server.

Validation included:

```powershell
Get-DnsClientServerAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
nslookup example.com
```

## Rollback

The workstation can return to DHCP-provided DNS with:

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ResetServerAddresses
Clear-DnsClientCache
```
