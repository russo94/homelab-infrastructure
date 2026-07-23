# Hardware Inventory

## Purpose

This document records the physical hardware used by the homelab.

It is the authoritative source for physical devices, hardware specifications, and their infrastructure roles.

---

## Compute Host

| Property | Value |
|----------|-------|
| Device | ASUS TUF Gaming FX505DT laptop |
| Role | Proxmox VE hypervisor |
| CPU | To be verified |
| Physical Cores | To be verified |
| Threads | To be verified |
| Installed RAM | To be verified |
| Integrated GPU | To be verified |
| Dedicated GPU | To be verified |
| Internal Storage | Documented in `inventory/storage.md` |
| Network Interfaces | To be verified |
| Firmware Version | To be verified |
| Production Status | Active |

---

## Router

| Property | Value |
|----------|-------|
| Device | ASUS ROG Rapture GT-BE98 |
| Role | Router, firewall, DHCP server, and VLAN gateway |
| Firmware Version | To be verified |
| Production Status | Active |

Detailed network design is documented under:

`docs/network/`

---

## Backup Hardware

| Property | Value |
|----------|-------|
| Device | External USB drive |
| Role | Homelab backup storage |
| Manufacturer | To be verified |
| Model | To be verified |
| Capacity | To be verified |
| Connection | USB |
| Filesystem | Documented in `inventory/storage.md` |
| Production Status | Active |

Backup implementation and restore mechanics are maintained in the separate `offsite-backup-v2` repository.

---

## Power Protection

| Component | Status |
|-----------|--------|
| Uninterruptible Power Supply | Not currently documented |
| Surge Protection | To be verified |
| Automatic Shutdown on Power Failure | Not currently configured or documented |

---

## Spare and Replacement Hardware

No spare infrastructure hardware is currently documented.

Potential future additions include:

- Replacement storage device
- Secondary backup drive
- Spare network adapter
- Replacement router configuration
- Uninterruptible power supply

---

## Documentation Rules

- Hardware specifications must be verified from the physical device or operating system.
- Storage layout belongs in `inventory/storage.md`.
- IP addresses belong in `inventory/ip-addresses.md`.
- VM and container resources belong in their respective inventory files.
- Serial numbers should not be committed unless there is a clear recovery or warranty-related need.
- Update this document whenever physical infrastructure is added, replaced, or retired.
