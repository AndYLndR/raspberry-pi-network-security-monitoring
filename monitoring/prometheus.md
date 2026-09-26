# Prometheus

## Purpose

Prometheus collects host metrics from Node Exporter.

## Scrape configuration

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: "raspberry-pi"
    static_configs:
      - targets:
          - "192.168.1.36:9100"
```

## Retention

```text
15 days
```

The retention window limits storage growth on the 32 GB microSD.

## Exposure model

Prometheus is not published directly to the LAN.

Grafana accesses it over the Docker network:

```text
http://prometheus:9090
```

## Target validation

The `raspberry-pi` target was verified as:

```text
UP
```

## Evidence

```text
screenshots/prometheus/prometheus-targets.png
```
