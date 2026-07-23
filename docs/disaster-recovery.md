# Disaster Recovery

## Purpose

This document defines the high-level recovery strategy for the homelab.

Its goal is to provide a clear recovery sequence following a complete or partial infrastructure failure.

Detailed recovery procedures for individual services are documented separately.

---

# Recovery Philosophy

The homelab is designed around the following principles:

- Recover infrastructure before applications.
- Restore services in dependency order.
- Verify each stage before continuing.
- Minimize manual configuration.
- Documentation is considered part of the recovery process.

---

# Recovery Scenarios

The recovery process depends on the scope of the failure.

Examples include:

- Complete Proxmox host failure
- Storage failure
- Router replacement
- Individual VM failure
- Individual LXC failure
- Service corruption
- Backup storage failure

Each scenario should follow the same dependency order.

---

# Recovery Order

The infrastructure should be restored in the following sequence.

## Phase 1 — Physical Infrastructure

- Restore or replace hardware.
- Install Proxmox VE.
- Configure storage.
- Configure networking.
- Verify Internet connectivity.

---

## Phase 2 — Network Infrastructure

Restore core networking.

- Router configuration
- VLANs
- DHCP
- DNS
- Tailscale connectivity

Network documentation:

`docs/network/`

---

## Phase 3 — Backup Access

Restore access to the backup repository.

Backup implementation:

`offsite-backup-v2`

Verify:

- Backup storage mounted
- Snapshots available
- Restore process tested

---

## Phase 4 — Core Infrastructure Services

Restore infrastructure services in dependency order.

Suggested order:

1. Pi-hole
2. NGINX Proxy Manager
3. Vaultwarden
4. Public Endpoints
5. Home Assistant

The exact restore procedure for each service is documented in its own service document.

---

## Phase 5 — Validation

Verify:

- DNS resolution
- Internet access
- HTTPS certificates
- Reverse proxy
- Remote access
- Application availability
- Scheduled backups

---

# Recovery Priorities

| Priority | Component |
|----------|-----------|
| Critical | Router |
| Critical | Proxmox VE |
| Critical | Storage |
| Critical | Backup Repository |
| High | Pi-hole |
| High | NGINX Proxy Manager |
| High | Vaultwarden |
| Medium | Public Endpoints |
| Medium | Home Assistant |

---

# Recovery Checklist

- Hardware operational
- Proxmox installed
- Storage mounted
- Network restored
- Tailscale operational
- Backup repository accessible
- Core services restored
- Certificates verified
- Backups resumed
- Documentation updated

---

# Documentation References

| Topic | Document |
|--------|----------|
| Architecture | `docs/architecture.md` |
| Network | `docs/network/` |
| Security | `docs/security.md` |
| Inventory | `inventory/` |
| Backup Implementation | `offsite-backup-v2` repository |
| Services | `docs/services/` |

---

# Documentation Rules

This document provides the overall recovery strategy.

Detailed implementation belongs in:

- Service documentation
- Operational procedures
- Backup documentation

Recovery information should not be duplicated across multiple documents.
