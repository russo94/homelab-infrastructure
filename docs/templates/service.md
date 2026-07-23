# Service Name

## Purpose

Describe what the service does and why it exists.

---

# Role in the Homelab

Explain why this service is part of the infrastructure.

Questions to answer:

- What problem does it solve?
- Why was this solution chosen?
- Is it critical?

---

# Deployment

| Property | Value |
|----------|-------|
| Type | VM / LXC |
| Host | Proxmox VE |
| Status | Production / Planned / Testing |
| Operating System | |
| Inventory | Reference inventory documents |

Deployment-specific information should be maintained in the inventory rather than duplicated here.

---

# Network

Document:

- Network location
- Access method
- Public or private
- Reverse proxy usage
- Tailscale access

IP addresses are maintained in:

`inventory/ip-addresses.md`

---

# Dependencies

List the services this service depends on.

Examples:

- Pi-hole
- NGINX Proxy Manager
- Tailscale
- Internet connectivity

---

# Dependents

List services that depend on this service.

---

# Data

Document:

- Persistent storage
- Configuration location
- Important files
- Volumes

---

# Backup

Document:

- Is it backed up?
- Backup frequency
- Backup repository

Implementation belongs in:

`offsite-backup-v2`

---

# Restore

Describe any service-specific restore considerations.

The overall recovery order is documented in:

`docs/disaster-recovery.md`

---

# Updates

Describe:

- Update method
- Expected downtime
- Verification after update

---

# Monitoring

Document how to verify the service is healthy.

Examples:

- Web UI
- Logs
- Systemd service
- Health endpoint

---

# Troubleshooting

Document common problems and their solutions.

This section should grow over time as operational experience is gained.

---

# Related Documentation

- Architecture
- Network
- Security
- Inventory
- Disaster Recovery
