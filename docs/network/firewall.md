# Firewall Policy

## Purpose

This document defines the network access policy between the Main LAN and the VLANs.

It describes the intended security model rather than router-specific implementation details.

---

## Design Principles

- Deny by default
- Least privilege
- Network segmentation
- Minimize lateral movement
- Explicitly allow only required traffic

---

## Network Access Matrix

| Source | Destination | Access |
|---------|-------------|--------|
| Main LAN | Internet | Allowed |
| Main LAN | VLAN 10 | Allowed |
| Main LAN | VLAN 20 | Allowed |
| Main LAN | VLAN 30 | Allowed |
| Main LAN | VLAN 40 | Allowed |
| Main LAN | VLAN 60 | Allowed |
| VLAN 10 | Main LAN | Allowed |
| VLAN 20 | Main LAN | Blocked |
| VLAN 30 | Main LAN | Blocked |
| VLAN 40 | Main LAN | Blocked |
| VLAN 60 | Main LAN | Blocked |

---

## Administrative Access

Infrastructure administration is performed exclusively through:

- Tailscale
- SSH public-key authentication
- HTTPS management interfaces

Administrative services are never exposed directly to the Internet.

---

## Internet Exposure

Only explicitly approved services may be published externally.

Current public services include:

- Vaultwarden
- Tesla Fleet public endpoint

All other services remain private.

---

## Future Improvements

Future versions of this document may include:

- Router firewall rules
- Inter-VLAN policies
- Port-level documentation
- Network diagrams
- IDS/IPS integration
