# Node Exporter

## Purpose

Node Exporter exposes Linux host metrics from the Raspberry Pi.

## Runtime

Node Exporter runs directly on the host as a systemd service.

## Version validated during deployment

```text
node_exporter 1.12.1
linux/arm64
```

## Listener

```text
192.168.1.36:9100
```

LAN clients are blocked from connecting directly by the host firewall.

## Metrics validated

- `node_cpu_seconds_total`
- `node_memory_MemAvailable_bytes`
- `node_memory_MemTotal_bytes`
- `node_filesystem_avail_bytes`
- `node_filesystem_size_bytes`
- `node_network_receive_bytes_total`
- `node_network_transmit_bytes_total`
- `node_boot_time_seconds`
- `node_hwmon_temp_celsius`
- `node_hwmon_fan_rpm`

The Raspberry Pi temperature and Active Cooler RPM were available through the normal `hwmon` collector, so no additional temperature exporter was required.
