# Containers Inventory

## Overview

This inventory contains all Linux containers running in the homelab.

It is the authoritative source for container deployment information.

---

## Linux Containers

| LXC ID | Hostname | Purpose | Operating System | IP Address | Status |
|-------:|----------|---------|------------------|------------|--------|
| 100 | `pihole` | DNS filtering and resolution | Debian | `192.168.50.52` | Production |
| 101 | `vaultwarden` | Password manager | Debian | `192.168.50.212` | Production |
| 102 | `nginxproxymanager` | Reverse proxy and TLS management | Debian | `192.168.50.87` | Production |
| 105 | `public-endpoints` | Public HTTPS endpoints | Debian 13 | `192.168.50.201` | Production |

---

## Notes

Container runtime information is managed by Proxmox VE.

Resource allocation details should be added when verified.

The authoritative sources are:

- This file for container identity and purpose
- `inventory/ip-addresses.md` for network addressing
- Service documentation for application details

---

## Documentation Rules

Update this file whenever:

- A container is created
- A container is removed
- A service is migrated
- Network addressing changes
- Production status changes
