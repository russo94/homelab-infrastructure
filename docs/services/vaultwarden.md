# Vaultwarden

## Purpose

Vaultwarden provides secure password management for the homelab.

It serves as the self-hosted Bitwarden-compatible password vault, allowing authorized users to securely store and synchronize credentials.

---

# Role in the Homelab

Vaultwarden is a critical infrastructure service.

It provides:

- Password management
- Secure credential storage
- Secret synchronization
- Self-hosted Bitwarden compatibility

Because Vaultwarden stores infrastructure credentials, its availability is considered high priority.

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

Vaultwarden is deployed on the Main LAN.

External access is provided through NGINX Proxy Manager using HTTPS.

IP addressing is documented in:

`inventory/ip-addresses.md`

---

# Dependencies

Vaultwarden depends on:

- Proxmox VE
- Router
- DNS
- Pi-hole
- NGINX Proxy Manager
- Internet connectivity
- Valid TLS certificates

---

# Dependents

Users and applications requiring stored credentials depend on Vaultwarden.

---

# Data

Important data includes:

- Password vault
- User accounts
- Attachments
- Configuration
- Encryption metadata

Persistent data must always be included in backups.

---

# Backup

Vaultwarden is included in the homelab backup strategy.

Backup implementation is documented in the `offsite-backup-v2` repository.

Because Vaultwarden contains critical secrets, restore procedures should be tested periodically.

---

# Restore

General recovery order is documented in:

`docs/disaster-recovery.md`

After restoring Vaultwarden, verify:

- HTTPS access
- User login
- Vault synchronization
- Stored attachments
- Mobile client connectivity

---

# Updates

Update during scheduled maintenance.

After updating, verify:

- Web interface
- Client synchronization
- HTTPS certificates
- Authentication
- Application logs

---

# Monitoring

Routine health checks include:

- Container running
- Web interface accessible
- HTTPS certificate valid
- Successful client synchronization
- No critical log errors

---

# Troubleshooting

Common checks include:

- Verify the container is running.
- Confirm reverse proxy configuration.
- Verify TLS certificate validity.
- Check Vaultwarden logs.
- Test login with a known account.
- Verify DNS resolution.

---

# Related Documentation

- `docs/architecture.md`
- `docs/network/`
- `docs/disaster-recovery.md`
- `docs/services/nginx-proxy-manager.md`
- `docs/services/pihole.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
