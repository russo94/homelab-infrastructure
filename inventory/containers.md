# Linux Containers

## Overview

This inventory contains all Linux containers running in the homelab.

| LXC ID | Hostname | Purpose | OS | vCPU | RAM | Disk | Status |
|-------:|----------|---------|----|:----:|:---:|:----:|--------|
| 100 | `pihole` | DNS filtering and local DNS | To be verified | To be verified | To be verified | To be verified | Production |
| 101 | `vaultwarden` | Password manager | To be verified | To be verified | To be verified | To be verified | Production |
| 102 | `nginx-proxy-manager` | Reverse proxy | To be verified | To be verified | To be verified | To be verified | Production |
| 105 | `public-endpoints` | Public static endpoints | To be verified | To be verified | To be verified | To be verified | Production |

---

## Notes

This inventory should be updated whenever a container is created, removed, or its resources are changed.

Hardware specifications should be verified from the Proxmox host rather than estimated.
