# DHCP

## Purpose

This document describes the DHCP architecture of the homelab.

It defines how IP addresses are assigned across the different network segments. IP assignments themselves are maintained in the inventory.

---

## DHCP Authority

The ASUS GT-BE98 router is the DHCP server for all network segments.

Each network has its own independent DHCP scope.

---

## DHCP Scope

| Network | DHCP | Notes |
|---------|------|-------|
| Main LAN | Enabled | Infrastructure network |
| VLAN 10 | Enabled | Trusted devices |
| VLAN 20 | Enabled | IoT devices |
| VLAN 30 | Enabled | Media devices |
| VLAN 40 | Enabled | Cameras |
| VLAN 60 | Enabled | Guest devices |

---

## Infrastructure Addressing

Infrastructure services use static assignments or DHCP reservations to ensure predictable management.

Examples include:

- Proxmox VE
- Pi-hole
- Vaultwarden
- NGINX Proxy Manager
- Tailscale Gateway
- Home Assistant
- Public Endpoints

The authoritative IP inventory is maintained in:

`inventory/ip-addresses.md`

---

## Design Principles

- Infrastructure addresses should remain stable.
- Client devices receive dynamic DHCP leases.
- Each VLAN has an independent DHCP scope.
- DHCP configuration should remain simple and centrally managed.
