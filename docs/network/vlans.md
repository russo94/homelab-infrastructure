# VLANs

## Purpose

This document defines the VLANs used in the homelab and their intended roles.

IP subnets and gateway addresses are maintained in:

`inventory/ip-addresses.md`

---

## VLAN Overview

| VLAN ID | SSID | Purpose | Main LAN Access |
|--------:|------|---------|-----------------|
| 10 | `Warcraft_Lordaeron` | Trusted personal devices | Allowed |
| 20 | `Warcraft_IoT` | IoT devices | Blocked |
| 30 | `Warcraft_Media` | TVs and media devices | Blocked |
| 40 | `Warcraft_Legion` | Cameras | Blocked |
| 60 | `Warcraft_Goldshire` | Guest devices | Blocked |

The Main LAN is used for infrastructure and servers and is not configured as VLAN 50.

---

## VLAN 10 — Trusted Devices

VLAN 10 is intended for trusted personal devices such as computers and administration clients.

Characteristics:

- May access infrastructure services on the Main LAN
- Uses Pi-hole for DNS
- Intended for trusted devices only

---

## VLAN 20 — IoT Devices

VLAN 20 is intended for Internet-connected household devices.

Characteristics:

- Blocked from the Main LAN
- DNS configuration depends on router configuration
- Intended to reduce the impact of insecure IoT devices

---

## VLAN 30 — Media Devices

VLAN 30 is intended for TVs, streaming devices, and other media equipment.

Characteristics:

- Blocked from the Main LAN
- DNS configuration depends on router configuration
- Separated from trusted personal devices

---

## VLAN 40 — Cameras

VLAN 40 is intended for cameras and surveillance-related devices.

Characteristics:

- Blocked from the Main LAN
- DNS configuration depends on router configuration
- Isolated from other infrastructure wherever possible

---

## VLAN 60 — Guest Devices

VLAN 60 is intended for visitors and untrusted temporary devices.

Characteristics:

- Internet access only
- Blocked from the Main LAN
- Uses Pi-hole DNS filtering
- Wireless access-point isolation enabled

---

## Policy

Only VLAN 10 is permitted to initiate connections to the Main LAN.

Detailed access-control rules are documented in:

`docs/network/firewall.md`
