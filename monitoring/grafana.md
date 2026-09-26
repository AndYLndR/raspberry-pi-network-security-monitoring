# Grafana

## Purpose

Grafana provides the primary metrics dashboard for the Raspberry Pi.

## Datasource

Prometheus:

```text
http://prometheus:9090
```

The connection uses Docker internal DNS rather than the LAN address.

## Dashboard

```text
Raspberry Pi - System Overview
```

## Panels and PromQL

### CPU Usage

```promql
100 - (avg(rate(node_cpu_seconds_total{job="raspberry-pi",mode="idle"}[5m])) * 100)
```

### RAM Usage

```promql
100 * (1 - (
  node_memory_MemAvailable_bytes{job="raspberry-pi"}
  /
  node_memory_MemTotal_bytes{job="raspberry-pi"}
))
```

### Root Filesystem Usage

```promql
100 * (
  1 -
  (
    node_filesystem_avail_bytes{
      job="raspberry-pi",
      mountpoint="/",
      fstype="ext4"
    }
    /
    node_filesystem_size_bytes{
      job="raspberry-pi",
      mountpoint="/",
      fstype="ext4"
    }
  )
)
```

### System Uptime

```promql
time() - node_boot_time_seconds{job="raspberry-pi"}
```

### CPU Temperature

```promql
node_hwmon_temp_celsius{
  job="raspberry-pi",
  chip="thermal_thermal_zone0",
  sensor="temp0"
}
```

### Active Cooler Fan

```promql
node_hwmon_fan_rpm{
  job="raspberry-pi",
  chip="platform_cooling_fan",
  sensor="fan1"
}
```

### Load Average

```promql
node_load1{job="raspberry-pi"}
```

### Network Receive

```promql
rate(node_network_receive_bytes_total{
  job="raspberry-pi",
  device="eth0"
}[5m])
```

### Network Transmit

```promql
rate(node_network_transmit_bytes_total{
  job="raspberry-pi",
  device="eth0"
}[5m])
```

## Design decision

The dashboard was built manually to demonstrate understanding of the underlying metrics and PromQL queries.

## Evidence

```text
screenshots/grafana/raspberry-pi-overview.png
```
