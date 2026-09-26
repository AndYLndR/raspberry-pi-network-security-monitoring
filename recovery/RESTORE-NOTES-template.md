# Recovery Notes Template

This template describes the structure used by the private recovery archive.

## Private backup content

- repository snapshot
- host configuration
- Docker volume archives
- private secrets
- version/network/service manifests
- SHA256 integrity manifest

## Recovery order

1. Install Raspberry Pi OS Lite 64-bit.
2. Configure hostname and LAN address.
3. Install Docker Engine and Compose.
4. Restore host configuration.
5. Restore Docker named volumes.
6. Restore repository.
7. Restore private environment files.
8. Reload systemd.
9. Start the stack.
10. Validate services and firewall behavior.

Do not commit private recovery archives or real secrets to GitHub.
