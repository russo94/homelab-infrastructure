# Network

## Overview

The homelab uses a segmented network design to separate trusted devices, infrastructure, IoT devices, media devices, cameras, and guests.

This document provides only the high-level network overview. Detailed configuration is maintained in the dedicated network documents.

---

## Core Network

| Property | Value |
|----------|-------|
| Router | ASUS GT-BE98 |
| Hypervisor Bridge | `vmbr0` |
| Infrastructure Network | Main LAN |

The Main LAN uses the `192.168.50.0/24` subnet.

> The number `50` is part of the addressing scheme. The Main LAN is not VLAN 50.

---

## Network Segments

| Segment | Purpose |
|---------|---------|
| Main LAN | Infrastructure and servers |
| VLAN 10 | Trusted personal devices |
| VLAN 20 | IoT devices |
| VLAN 30 | Media devices |
| VLAN 40 | Cameras |
| VLAN 60 | Guest devices |

VLAN 10 is permitted to access infrastructure services on the Main LAN.

Infrastructure services on the Main LAN communicate according to required service dependencies.

Exact subnet, gateway, and host assignments are maintained in:

`inventory/ip-addresses.md`

---

## Remote Administration

Remote administration is performed through Tailscale.

SSH is not exposed directly to the Internet, and router port forwarding is not used for administrative access.

Detailed Tailscale gateway documentation is maintained in:

`docs/services/tailscale-gateway.md`

---

## Proxmox Networking

Proxmox guests connect through the `vmbr0` Linux bridge.

Guest-specific network configuration belongs in the VM and container inventories or the relevant service documentation.

---

## Detailed Documentation

| Topic | Document |
|-------|----------|
| VLAN definitions | `docs/network/vlans.md` |
| Access-control policy | `docs/network/firewall.md` |
| DNS architecture | `docs/network/dns.md` |
| DHCP architecture | `docs/network/dhcp.md` |
| Routing | `docs/network/routing.md` |
| IP assignments | `inventory/ip-addresses.md` |

---

## Network Principles

- Infrastructure services remain on the trusted Main LAN.
- VLAN 10 may access infrastructure services according to firewall policy.
- Other VLANs are isolated from infrastructure.
- Remote administration uses Tailscale.
- SSH is never exposed through router port forwarding.
- Host IP assignments are documented only in the IP inventory.
