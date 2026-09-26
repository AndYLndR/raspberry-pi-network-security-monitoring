# Raspberry Pi OS Setup

## Platform

```text
Raspberry Pi 5
4 GB RAM
SanDisk 32 GB microSD
Active Cooler
```

## Operating system

Raspberry Pi OS Lite 64-bit was selected.

The installed system reported:

```text
Debian GNU/Linux 13 (trixie)
aarch64
```

## Initial configuration

The system was prepared with:

- hostname: `rpi-monitor`
- non-root administrative user: `piadmin`
- SSH enabled
- Ethernet as primary network interface
- Wi-Fi unused
- timezone configured locally

## Initial baseline checks

Useful validation commands included:

```bash
hostname
whoami
uname -m
cat /etc/os-release
free -h
lsblk
ip -br addr
vcgencmd measure_temp
```

## Updates

The system was updated using normal APT packages:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove --purge -y
```

`rpi-update` was intentionally not used.

## Evidence

See:

```text
screenshots/system/raspberry-pi-system-info.png
```
