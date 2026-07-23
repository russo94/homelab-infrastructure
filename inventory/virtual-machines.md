# Virtual Machines Inventory

## Overview

This inventory contains all virtual machines running in the homelab.

It is the authoritative source for VM deployment information.

---

## Virtual Machines

| VM ID | Hostname | Purpose | Operating System | RAM | Disk | Status |
|------:|----------|---------|------------------|-----|------|--------|
| 103 | `home-assistant` | Home automation platform | To be verified | 4096 MB | 32 GB | Production |
| 104 | `ts-gateway-01` | Secure remote administration gateway | Debian 13.6 | 1024 MB | 8 GB | Production |

---

## Notes

Virtual machine runtime information is managed by Proxmox VE.

Additional resource details should be added when verified.

The authoritative sources are:

- This file for VM identity and purpose
- `inventory/ip-addresses.md` for network addressing
- Service documentation for application details

---

## Documentation Rules

Update this file whenever:

- A VM is created
- A VM is removed
- A service is migrated
- Network addressing changes
- Hardware resources change
- Production status changes
