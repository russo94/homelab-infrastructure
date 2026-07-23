# NGINX Proxy Manager

## Purpose

NGINX Proxy Manager provides reverse proxy functionality and TLS certificate management for publicly accessible services.

It acts as the entry point for services exposed through HTTPS.

---

# Deployment

| Property | Value |
|----------|-------|
| Type | LXC Container |
| Container ID | `102` |
| Hostname | `nginxproxymanager` |
| IP Address | `192.168.50.87` |
| Network | Main LAN |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/containers.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

NGINX Proxy Manager provides:

- Reverse proxying
- HTTPS termination
- TLS certificate management
- Public service routing

Current intended public access flow:

```text
Internet
   |
   v
Cloudflare
   |
   v
NGINX Proxy Manager
   |
   +--> Vaultwarden
   |
   +--> Public Endpoints
```

Detailed proxy host configuration should be verified from NGINX Proxy Manager.

---

# Deployment Architecture

NGINX Proxy Manager is installed directly inside the LXC container.

It is not running through Docker.

Application components:

```text
LXC 102
 |
 ├── npm.service
 |
 └── openresty.service
```

---

# Installation Paths

Verified paths:

```text
/opt/nginxproxymanager
/opt/certbot
```

---

# Network Configuration

Listening ports:

| Port | Protocol | Purpose |
|------|----------|---------|
| 80 | TCP | HTTP |
| 81 | TCP | Administration interface |
| 443 | TCP | HTTPS |

---

# Dependencies

NGINX Proxy Manager depends on:

- Proxmox VE
- Network availability
- DNS resolution
- Cloudflare configuration
- TLS certificate system

---

# Dependents

Services depending on NGINX Proxy Manager:

- Vaultwarden
- Public endpoints

---

# Persistent Data

Important data includes:

- Proxy host configurations
- SSL certificates
- Access lists
- User configuration
- Application database

Persistent data must be included in backups.

---

# Backup

Backup strategy:

`offsite-backup-v2`

Recovery must include:

- NGINX Proxy Manager configuration
- Certificate data
- Proxy host definitions

---

# Restore Procedure

General recovery order:

`docs/disaster-recovery.md`

After restoring:

1. Start the container.
2. Verify npm service.
3. Verify OpenResty service.
4. Verify ports 80/81/443.
5. Test HTTPS access.

---

# Verification

Last verified:

2026-07-23

Checks performed:

## Network

Command:

```bash
pct exec 102 -- ip addr
```

Result:

```text
192.168.50.87/24
```

---

## Services

Command:

```bash
systemctl list-units --type=service | grep -i npm
```

Result:

```text
npm.service active running
```

Command:

```bash
systemctl list-units --type=service | grep -i open
```

Result:

```text
openresty.service active running
```

---

## Ports

Command:

```bash
ss -tulpn | grep -E ":80|:81|:443"
```

Result:

```text
80  HTTP
81  Administration
443 HTTPS
```

---

# Troubleshooting

Check NGINX Proxy Manager:

```bash
systemctl status npm
```

Check OpenResty:

```bash
systemctl status openresty
```

Check ports:

```bash
ss -tulpn | grep -E ":80|:81|:443"
```

---

# Related Documentation

- `docs/services/vaultwarden.md`
- `docs/services/public-endpoints.md`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
