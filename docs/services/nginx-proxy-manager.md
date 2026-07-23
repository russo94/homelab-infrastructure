# NGINX Proxy Manager

## Purpose

NGINX Proxy Manager provides reverse proxy services for the homelab.

It securely publishes selected internal services using HTTPS while managing SSL/TLS certificates and proxy routing.

---

# Role in the Homelab

NGINX Proxy Manager acts as the public entry point for services that are intentionally exposed outside the local network.

It provides:

- Reverse proxy
- HTTPS termination
- Automatic certificate management
- Centralized access to published services

---

# Deployment

| Property | Value |
|----------|-------|
| Type | LXC |
| Host | Proxmox VE |
| Status | Production |
| Operating System | Debian |
| Inventory | See `inventory/containers.md` |

Deployment-specific information such as container ID, CPU, memory, and IP address is maintained in the inventory.

---

# Network

NGINX Proxy Manager is deployed on the Main LAN.

It receives inbound HTTPS traffic and forwards requests to internal services.

Public access is restricted to services intentionally published.

IP addressing is documented in:

`inventory/ip-addresses.md`

---

# Dependencies

NGINX Proxy Manager depends on:

- Proxmox VE
- Router
- Internet connectivity
- DNS
- Valid TLS certificates

---

# Dependents

Services currently published through NGINX Proxy Manager include:

- Vaultwarden

Additional services may be added as the homelab grows.

---

# Data

Important data includes:

- Proxy Hosts
- SSL certificates
- Access Lists
- Hosts configuration
- Redirection rules

Persistent configuration should be included in backups.

---

# Backup

NGINX Proxy Manager is included in the homelab backup strategy.

Backup implementation is documented in the `offsite-backup-v2` repository.

---

# Restore

General recovery order is documented in:

`docs/disaster-recovery.md`

After restoring NGINX Proxy Manager, verify:

- Web interface
- HTTPS certificates
- Proxy hosts
- DNS resolution
- External accessibility

---

# Updates

Update during planned maintenance.

After updating, verify:

- Web interface
- HTTPS access
- Certificate renewal
- Proxy routing
- Published services

---

# Monitoring

Routine health checks include:

- Container running
- Web interface accessible
- Certificates valid
- Proxy hosts online
- No critical log errors

---

# Troubleshooting

Common checks include:

- Verify the container is running.
- Verify ports 80 and 443 are reachable.
- Check certificate status.
- Confirm DNS records.
- Verify backend services are reachable.
- Review NGINX Proxy Manager logs.

---

# Related Documentation

- `docs/architecture.md`
- `docs/network/`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
