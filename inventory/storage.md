# Storage Inventory

## Purpose

This document records storage devices used by the homelab.

It is the authoritative source for physical storage devices, filesystems, mount points, and storage roles.

---

# Internal Storage

## Proxmox System Disk

| Property | Value |
|----------|-------|
| Device | NVMe SSD |
| Capacity | ~477 GB |
| Role | Proxmox VE system and VM/LXC storage |
| Device Name | `nvme0n1` |
| Storage Type | LVM |
| Status | Active |

---

## Partition Layout

| Partition | Size | Purpose |
|-----------|------|---------|
| `nvme0n1p1` | ~1 MB | EFI metadata |
| `nvme0n1p2` | 1 GB | EFI boot partition |
| `nvme0n1p3` | ~476 GB | Proxmox LVM storage |

---

## Proxmox LVM Layout

| Logical Volume | Size | Purpose |
|----------------|------|---------|
| `pve-root` | 96 GB | Proxmox operating system |
| `pve-swap` | 8 GB | Swap |
| `pve-data` | ~349 GB | VM and container storage |

---

# Virtual Machine Storage

| ID | Service | Disk Allocation |
|----|---------|----------------|
| 100 | Pi-hole | 2 GB |
| 101 | Vaultwarden | 20 GB |
| 102 | NGINX Proxy Manager | 8 GB |
| 103 | Home Assistant | 32 GB |
| 104 | Tailscale Gateway | 8 GB |
| 105 | Public Endpoints | 4 GB |

---

# Backup Storage

## External USB Backup Disk

| Property | Value |
|----------|-------|
| Device | USB external storage |
| Device Name | `sda` |
| Capacity | ~120 GB |
| Mount Point | `/mnt/offsite-backup` |
| Role | Offsite backup storage |
| Filesystem | To be verified |
| Status | Active |

Backup implementation is documented in:

`offsite-backup-v2`

---

# Storage Rules

- Production data must have a documented backup strategy.
- Storage changes must be documented before removing old devices.
- Disk replacements should include verification of restore procedures.
- VM and container storage allocation changes should be reflected in inventory.

---

# Documentation Rules

Update this file whenever:

- A disk is added
- A disk is removed
- Storage is expanded
- Mount points change
- Backup devices change
- Filesystems are modified
