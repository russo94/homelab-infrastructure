# Routing

## Purpose

This document describes how traffic flows between the Internet, the Main LAN, and the VLANs.

It documents the intended routing architecture rather than device-specific router configuration.

---

## Routing Overview

The ASUS GT-BE98 is the default gateway for all networks.

It is responsible for:

- Routing traffic between local networks
- Providing Internet access
- Enforcing network isolation
- Acting as the DHCP server
- Providing the default DNS configuration

---

## Network Topology

                    Internet
                        |
                        v
                 ASUS GT-BE98
                        |
        +---------------+---------------+
        |               |               |
        v               v               v
    Main LAN       User VLANs       Guest VLAN
 192.168.50.0     10/20/30/40          60

---

## Routing Policy

| Source | Destination | Routing |
|--------|-------------|---------|
| Main LAN | Internet | Allowed |
| Main LAN | VLANs | Configuration not verified |
| VLAN 10 | Main LAN | Allowed |
| VLAN 20 | Main LAN | Blocked |
| VLAN 30 | Main LAN | Blocked |
| VLAN 40 | Main LAN | Blocked |
| VLAN 60 | Main LAN | Blocked |
| All Networks | Internet | Allowed |

---

## Administrative Traffic

Infrastructure administration is performed through:

- Tailscale
- SSH
- HTTPS

Administrative traffic originates from trusted devices on the Main LAN or VLAN 10.

---

## Design Principles

- Centralized routing through the router
- Minimize east-west traffic between network segments
- Keep infrastructure isolated from untrusted devices
- Allow only explicitly required inter-network communication
