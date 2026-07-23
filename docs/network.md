# Network

## Overview

The homelab uses a segmented network design to separate trusted devices from IoT, media devices, cameras, and guests.

The primary LAN subnet is:

| Property | Value |
|----------|-------|
| Subnet | `192.168.50.0/24` |
| Router | ASUS GT-BE98 |
| Hypervisor Bridge | `vmbr0` |

> **Important:** The LAN subnet (`192.168.50.0/24`) is **not** VLAN 50. The number `50` is part of the IP addressing scheme only.

---

## VLAN Layout

| VLAN | Purpose | Access |
|------|---------|--------|
| Main LAN | Infrastructure and servers | Full internal access |
| 10 | Personal computers | Access to internal services |
| 20 | IoT devices | Restricted |
| 30 | TVs & Media | Restricted |
| 40 | Cameras | Isolated |
| 60 | Guest network | Internet only |

Only VLAN 10 is permitted to access infrastructure services hosted on the main LAN.

---

## Infrastructure Network

Current infrastructure services:

| Host | Address | Notes |
|------|---------|-------|
| Proxmox Host | *(Document when desired)* | Hypervisor |
| ts-gateway-01 | `192.168.50.193` | Remote administration gateway |

---

## Tailscale

The remote administration gateway also participates in the private Tailscale network.

| Property | Value |
|----------|-------|
| Hostname | `ts-gateway-01` |
| LAN Address | `192.168.50.193` |
| Tailscale Address | `100.68.131.104` |
| MagicDNS | Enabled |

Remote administration is performed through the Tailscale network instead of exposing SSH directly to the Internet.

---

## Proxmox Networking

The Tailscale gateway VM is connected using:

| Setting | Value |
|---------|-------|
| Bridge | `vmbr0` |
| Model | VirtIO |
| VLAN Tag | None |

No VLAN tag is configured on the VM network interface.

---

## Network Principles

- Infrastructure services remain on the trusted LAN.
- Remote administration uses Tailscale.
- SSH is never exposed through router port forwarding.
- Network segmentation reduces lateral movement between device categories.
- Future expansion should preserve clear separation between infrastructure and client devices.
