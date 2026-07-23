# Hardware Inventory

## Purpose

This document records the physical hardware used by the homelab.

It is the authoritative source for physical devices, hardware specifications, and their infrastructure roles.

---

# Compute Host

| Property | Value |
|----------|-------|
| Device | ASUS TUF Gaming FX505DT laptop |
| Role | Proxmox VE hypervisor |
| CPU | AMD Ryzen 5 3550H with Radeon Vega Mobile Gfx |
| Physical Cores | 4 |
| Threads | 8 |
| Installed RAM | 14 GB |
| Integrated GPU | AMD Radeon Vega Mobile Graphics |
| Dedicated GPU | NVIDIA GeForce GTX 1650 Mobile / Max-Q |
| Internal Storage | Micron 2200V NVMe 512 GB SSD |
| Network Interfaces | Gigabit Ethernet (`nic0`), WiFi (`wlp4s0`) |
| BIOS Version | FX505DT.315 |
| BIOS Release Date | 2020-09-22 |
| Virtualization | AMD-V enabled |
| Proxmox VE Version | 9.2.4 |
| Kernel | 7.0.14-5-pve |
| Production Status | Active |

---

# Router

| Property | Value |
|----------|-------|
| Device | ASUS ROG Rapture GT-BE98 |
| Role | Router, firewall, DHCP server, and VLAN gateway |
| Firmware Version | To be verified |
| Production Status | Active |

Detailed network design is documented under:

`docs/network/`

---

# Backup Hardware

| Property | Value |
|----------|-------|
| Device | External USB drive |
| Role | Homelab backup storage |
| Manufacturer | To be verified |
| Model | To be verified |
| Capacity | 120 GB class device |
| Connection | USB |
| Mount Point | `/mnt/offsite-backup` |
| Filesystem | Documented in `inventory/storage.md` |
| Production Status | Active |

Backup implementation and restore mechanics are maintained in the separate `offsite-backup-v2` repository.

---

# Power Protection

| Component | Status |
|-----------|--------|
| Uninterruptible Power Supply | Not currently documented |
| Surge Protection | To be verified |
| Automatic Shutdown on Power Failure | Not currently configured or documented |

---

# Spare and Replacement Hardware

No spare infrastructure hardware is currently documented.

Potential future additions include:

- Replacement storage device
- Secondary backup drive
- Spare network adapter
- Replacement router configuration
- Uninterruptible power supply

---

# Documentation Rules

- Hardware specifications must be verified from the physical device or operating system.
- Storage layout belongs in `inventory/storage.md`.
- IP addresses belong in `inventory/ip-addresses.md`.
- VM and container resources belong in their respective inventory files.
- Serial numbers should not be committed unless there is a clear recovery or warranty-related need.
- Update this document whenever physical infrastructure is added, replaced, or retired.
