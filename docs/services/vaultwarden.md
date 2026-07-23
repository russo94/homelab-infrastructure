# Vaultwarden

## Purpose

Vaultwarden provides a self-hosted Bitwarden-compatible password management service for the homelab.

It stores and manages credentials securely while providing access through the homelab reverse proxy infrastructure.

---

# Deployment

| Property | Value |
|----------|-------|
| Type | LXC Container |
| Container ID | `101` |
| Hostname | `vaultwarden` |
| IP Address | `192.168.50.212` |
| Network | Main LAN |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/containers.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

Vaultwarden provides:

- Password management
- Bitwarden-compatible vault access
- Secure credential storage

Vaultwarden is a critical infrastructure service because it stores user and infrastructure credentials.

Public access is intended to be provided through NGINX Proxy Manager.

Current intended access flow:

```text
Internet
   |
   v
Cloudflare
   |
   v
NGINX Proxy Manager
   |
   v
Vaultwarden
192.168.50.212:8000
```

Detailed proxy configuration should be verified from NGINX Proxy Manager.

---

# Deployment Architecture

Vaultwarden is installed directly inside the LXC container.

It is not running through Docker.

Architecture:

```text
LXC 101
 |
 └── vaultwarden.service
        |
        └── /opt/vaultwarden/bin/vaultwarden
```

---

# Application Paths

Verified paths:

| Path | Purpose |
|------|---------|
| `/opt/vaultwarden/bin/vaultwarden` | Vaultwarden application binary |
| `/opt/vaultwarden/data` | Database and persistent application data |
| `/opt/vaultwarden/web-vault` | Web vault files |
| `/opt/vaultwarden/.env` | Application configuration |
| `/opt/vaultwarden/backups` | Local application backups |

---

# Configuration

Vaultwarden configuration is stored in:

```text
/opt/vaultwarden/.env
```

Secrets must never be committed to Git.

Important verified settings:

```text
ROCKET_ADDRESS=0.0.0.0

DATA_FOLDER=/opt/vaultwarden/data

DATABASE_MAX_CONNS=10

WEB_VAULT_FOLDER=/opt/vaultwarden/web-vault

WEB_VAULT_ENABLED=true

SIGNUPS_ALLOWED=false
```

User registration is disabled.

---

# Storage

Vaultwarden persistent data is stored in:

```text
/opt/vaultwarden/data
```

Verified contents include:

```text
db.sqlite3
db.sqlite3-shm
db.sqlite3-wal
rsa_key.pem
icon_cache/
tmp/
```

Critical recovery data:

- SQLite database
- RSA key
- Attachments
- Application state

---

# Network Configuration

Vaultwarden listens on:

| Port | Protocol | Purpose |
|------|----------|---------|
| 8000 | TCP | Vaultwarden application |

The service is published externally through the reverse proxy layer.

---

# Dependencies

Vaultwarden depends on:

- Proxmox VE
- Network availability
- DNS resolution
- NGINX Proxy Manager
- TLS certificates
- Persistent storage

---

# Backup

Vaultwarden has local application backups.

Location:

```text
/opt/vaultwarden/backups
```

Verified backup files exist.

The homelab backup strategy is documented in:

```text
offsite-backup-v2
```

Required backup data:

```text
/opt/vaultwarden/data
/opt/vaultwarden/.env
/opt/vaultwarden/web-vault
/opt/vaultwarden/bin
```

Secrets contained in configuration files must remain protected.

---

# Restore Procedure

General recovery order:

`docs/disaster-recovery.md`

After restoring:

1. Restore Vaultwarden data.
2. Restore configuration.
3. Verify file ownership.
4. Start Vaultwarden service.
5. Verify application availability.
6. Test login functionality.

---

# Verification

Last verified:

2026-07-23

Checks performed:

## Network

Command:

```bash
pct exec 101 -- ip addr
```

Result:

```text
192.168.50.212/24
```

---

## Service Status

Command:

```bash
pct exec 101 -- systemctl list-units --type=service | grep -i vault
```

Result:

```text
vaultwarden.service active running
```

---

## Application Process

Command:

```bash
pct exec 101 -- ps aux | grep -v grep | grep -i vault
```

Result:

```text
/opt/vaultwarden/bin/vaultwarden
```

---

## Listening Port

Command:

```bash
pct exec 101 -- ss -tulpn
```

Result:

```text
0.0.0.0:8000
```

---

# Troubleshooting

Check service:

```bash
systemctl status vaultwarden
```

Restart service:

```bash
systemctl restart vaultwarden
```

Check logs:

```bash
journalctl -u vaultwarden
```

Check listening port:

```bash
ss -tulpn | grep 8000
```

---

# Security Notes

Never commit:

- `.env`
- Admin token
- Private keys
- Database files
- Backup archives

Only document:

- File locations
- Configuration purpose
- Recovery procedures

---

# Related Documentation

- `docs/services/nginx-proxy-manager.md`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
