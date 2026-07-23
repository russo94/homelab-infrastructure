# Storage Inventory

## Purpose

This document records the storage devices used by the homelab.

It is the authoritative source for physical storage devices, filesystems, mount points, and their intended purpose.

---

# Proxmox System Storage

| Property | Value |
|----------|-------|
| Device | To be verified |
| Purpose | Proxmox operating system and virtual workloads |
| Capacity | To be verified |
| Filesystem | To be verified |
| Mount Point | `/` |
| Production Status | Active |

---

# Backup Storage

| Property | Value |
|----------|-------|
| Device | External USB Drive |
| Purpose | Offsite Backup Repository |
| Capacity | To be verified |
| Filesystem | To be verified |
| Mount Point | To be verified |
| Production Status | Active |

This storage is used exclusively by the **offsite-backup-v2** project.

---

# Storage Layout

| Storage | Purpose |
|---------|---------|
| Proxmox System Storage | Hypervisor, VMs, and Linux Containers |
| External USB Storage | Offsite backups |

---

# Backup Repository

The backup implementation is documented in the **offsite-backup-v2** repository.

This repository documents:

- where backups are stored
- what depends on the storage
- disaster recovery order

It does **not** duplicate backup implementation details.

---

# Future Storage

Potential future additions:

- NAS
- Secondary backup disk
- Cloud backup
- ZFS storage
- Replication target

---

# Documentation Rules

- Device names should be verified from the operating system.
- UUIDs should be documented when useful for recovery.
- Mount points should always reflect the production environment.
- Backup implementation belongs in the backup repository.
- Update this document whenever storage devices are added, removed, reformatted, or repurposed.
