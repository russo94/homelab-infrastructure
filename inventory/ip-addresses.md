# IP Address Inventory

## Purpose

This document is the authoritative inventory of IP address assignments within the homelab.

Network architecture and VLAN design are documented separately under `docs/network/`.

---

## Infrastructure

| Hostname | Type | LAN IP | Tailscale IP | Purpose |
|----------|------|--------|--------------|---------|
| `proxmox` | Hypervisor | To be verified | N/A | Proxmox VE host |
| `ts-gateway-01` | VM | `192.168.50.193` | `100.68.131.104` | Secure remote administration gateway |
| `pihole` | LXC | `192.168.50.52` | N/A | DNS server |
| `vaultwarden` | LXC | `192.168.50.212` | N/A | Password manager |
| `nginx-proxy-manager` | LXC | `192.168.50.87` | N/A | Reverse proxy |
| `home-assistant` | VM | `192.168.50.194` | N/A | Home automation |
| `public-endpoints` | LXC | `192.168.50.201` | N/A | Public endpoints |

---

## Networks

| Network | Subnet | Gateway |
|---------|--------|---------|
| Main LAN | `192.168.50.0/24` | `192.168.50.1` |
| VLAN 10 | `192.168.10.0/24` | `192.168.10.1` |
| VLAN 20 | `192.168.20.0/24` | `192.168.20.1` |
| VLAN 30 | `192.168.30.0/24` | `192.168.30.1` |
| VLAN 40 | `192.168.40.0/24` | `192.168.40.1` |
| VLAN 60 | `192.168.60.0/24` | `192.168.60.1` |

---

## Notes

- This document is the authoritative source for IP address assignments.
- Service documentation should reference this document rather than duplicate IP addresses.
- Update this file whenever an address assignment changes.
