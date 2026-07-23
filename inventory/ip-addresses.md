# IP Address Inventory

## Purpose

This document is the authoritative source for infrastructure IP addresses.

All services, virtual machines, and containers should reference this document instead of maintaining their own IP address lists.

---

# Infrastructure

| Hostname | Type | ID | LAN IP | Purpose |
|----------|------|----|--------|---------|
| `pihole` | LXC | 100 | `192.168.50.52` | DNS filtering and resolution |
| `nginxproxymanager` | LXC | 102 | `192.168.50.87` | Reverse proxy |
| `ts-gateway-01` | VM | 104 | `192.168.50.193` | Remote administration gateway |
| `home-assistant` | VM | 103 | `192.168.50.194` | Home automation |
| `public-endpoints` | LXC | 105 | `192.168.50.201` | Public HTTPS endpoints |
| `vaultwarden` | LXC | 101 | `192.168.50.212` | Password manager |

---

# Network Addressing

| Network | Subnet | Gateway |
|----------|--------|---------|
| Main LAN | `192.168.50.0/24` | `192.168.50.1` |

---

# Tailscale

| Hostname | LAN IP | Tailscale IP |
|----------|--------|--------------|
| `ts-gateway-01` | `192.168.50.193` | `100.68.131.104` |

---

# Notes

IP addresses should remain stable for infrastructure services.

Infrastructure addresses should use:

- Static assignments
- DHCP reservations
- Or another documented method

Client device addressing is not maintained here.

---

# Documentation Rules

Update this file whenever:

- A VM changes IP address
- A container changes IP address
- A service is migrated
- A new infrastructure service is deployed
- A device is removed

This file should always represent the current production network state.
