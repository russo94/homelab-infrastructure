# Homelab Architecture

## Overview

This document provides a high-level overview of the homelab infrastructure.

Detailed implementation, configuration, and operational procedures are documented in the individual service and infrastructure documents.

---

## Physical Infrastructure

| Component | Description |
|-----------|-------------|
| Host | ASUS TUF FX505DT Laptop |
| Hypervisor | Proxmox VE |
| Router | ASUS GT-BE98 |
| Backup Storage | USB External Drive |

---

## Network

| Network | Purpose |
|---------|---------|
| Main LAN | Infrastructure and servers |
| VLAN 10 | Personal Devices |
| VLAN 20 | IoT Devices |
| VLAN 30 | Media Devices |
| VLAN 40 | Cameras |
| VLAN 60 | Guest Network |

---

## Compute

| ID | Type | Name | IP Address | Purpose |
|----|------|------|------------|---------|
| 100 | LXC | Pi-hole | 192.168.50.52 | DNS Server |
| 101 | LXC | Vaultwarden | 192.168.50.212 | Password Manager |
| 102 | LXC | NGINX Proxy Manager | 192.168.50.87 | Reverse Proxy |
| 103 | VM | Home Assistant | 192.168.50.194 | Home Automation |
| 104 | VM | Tailscale Gateway | 192.168.50.193 | Secure Remote Access |
| 105 | LXC | public-endpoints | 192.168.50.201 | Public Endpoints |

---

## Public Services

| Service | Public | Access |
|---------|--------|--------|
| Vaultwarden | Yes | Cloudflare → NGINX Proxy Manager |
| Tesla Fleet Public Key | Yes | public-endpoints |
| Home Assistant | No | Accessible only through Tailscale |

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
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
   Vaultwarden             public-endpoints
                                      │
                                      ▼
                         Tesla Fleet Public Key

────────────────────────────────────────────────

              Proxmox VE Hypervisor

   LXC 100  Pi-hole
   LXC 101  Vaultwarden
   LXC 102  NGINX Proxy Manager
   VM  103  Home Assistant
   VM  104  Tailscale Gateway
   LXC 105  public-endpoints
```

---

## Documentation

| Document | Description |
|----------|-------------|
| `docs/network.md` | Network topology and VLAN configuration |
| `docs/security.md` | Security policies and hardening |
| `docs/services/` | Individual service documentation |
| `docs/integrations/` | Third-party integrations |
| `docs/adr/` | Architecture Decision Records |
