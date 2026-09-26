# Docker Setup

## Installation model

Docker Engine and the Docker Compose plugin were installed from Docker's official Debian repository for ARM64.

Validated platform:

```text
linux/arm64
```

## Installed components

- Docker Engine
- Docker CLI
- containerd
- Buildx plugin
- Docker Compose plugin

## Validation

The installation was validated using:

```bash
sudo docker version
sudo docker compose version
sudo docker run --rm hello-world
```

## Administrative access

The `piadmin` account was deliberately not added to the `docker` group.

Commands are executed with `sudo`.

## Logging configuration

`/etc/docker/daemon.json`:

```json
{
  "log-driver": "local",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  }
}
```

The goal is to avoid unbounded container log growth on microSD storage.

## User-defined network

Application services share a Docker network named:

```text
monitoring
```

Prometheus is intentionally reachable by Grafana only over this internal network.
