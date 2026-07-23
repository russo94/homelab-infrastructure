# Homelab Architecture

## Overview

This document describes the high-level architecture of the homelab.

It explains how the infrastructure is organized and how the major components interact. Deployment-specific details such as IP addresses, VM IDs, container IDs, and resource allocations are maintained in the inventory.

---

## Physical Infrastructure

| Component | Description |
|-----------|-------------|
| Host | ASUS TUF FX505DT laptop |
| Hypervisor | Proxmox VE |
| Router | ASUS GT-BE98 |
| Backup Storage | USB external drive |

---

## Network Design

The homelab uses segmented networking to separate infrastructure, trusted devices, IoT devices, media devices, cameras, and guests.

The network consists of:

- Main LAN for infrastructure and servers
- VLAN 10 for trusted personal devices
- VLAN 20 for IoT devices
- VLAN 30 for media devices
- VLAN 40 for cameras
- VLAN 60 for guest devices

Only VLAN 10 is permitted to access infrastructure services on the Main LAN.

Detailed network documentation is maintained under:

`docs/network/`

---

## Compute Platform

The infrastructure runs on Proxmox VE and consists of a combination of virtual machines and Linux containers.

Current deployment information is maintained in:

- `inventory/virtual-machines.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`

The inventory is the authoritative source for:

- VM and container IDs
- Hostnames
- IP addresses
- Operating systems
- Resource allocations
- Deployment status

---

## Remote Administration

Remote administration is performed through Tailscale.

Administrative services such as SSH are not exposed directly to the Internet.

The Tailscale gateway provides secure remote access to internal infrastructure.

Detailed documentation is maintained in:

`docs/services/tailscale-gateway.md`

---

## Public Services

Only explicitly approved services are exposed to the Internet.

Current public services include:

- Vaultwarden
- Tesla Fleet public endpoint

External traffic follows this path:

```text
Internet
   │
   ▼
Cloudflare
   │
   ▼
NGINX Proxy Manager
   │
   ├── Vaultwarden
   │
   └── Public Endpoints
```

All other services remain accessible only through the private network or Tailscale.

---

## Service Relationships

```text
                    Internet
                        │
                        ▼
                   Cloudflare
                        │
                        ▼
              NGINX Proxy Manager
                   │         │
                   ▼         ▼
             Vaultwarden  Public Endpoints

────────────────────────────────────────────

                 Proxmox VE Host
                        │
             ┌──────────┴──────────┐
             ▼                     ▼
      Virtual Machines      Linux Containers
             │                     │
             └──────────┬──────────┘
                        ▼
                Internal Services
                        │
                        ▼
                 Tailscale Access
```

---

## Backup Architecture

The homelab uses an external USB drive connected to the Proxmox host for backup storage.

Backup implementation, retention, automation, and restore mechanics are maintained in the separate repository:

`offsite-backup-v2`

This repository documents how the backup system fits into the homelab and the order in which services should be restored.

---

## Documentation Structure

| Topic | Location |
|-------|----------|
| Network | `docs/network/` |
| Security | `docs/security.md` |
| Inventory | `inventory/` |
| Services | `docs/services/` |
| Integrations | `docs/integrations/` |
| Architecture decisions | `docs/adr/` |
| Diagrams | `diagrams/` |
| Backup implementation | `offsite-backup-v2` repository |

---

## Design Principles

- Single source of truth
- Separation of concerns
- Least privilege
- Minimal public exposure
- Recovery-first documentation
- Modular and maintainable design
- Verified facts instead of assumptions
