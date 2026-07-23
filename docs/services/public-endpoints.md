# Public Endpoints

## Purpose

Public Endpoints provides a dedicated static web service for files that require public HTTPS access.

Its purpose is to expose verification files without directly exposing internal homelab services.

The service currently hosts the Tesla Fleet API public key endpoint.

---

# Deployment

| Property | Value |
|-----------|-------|
| Type | LXC Container |
| Container ID | `105` |
| Hostname | `public-endpoints` |
| Operating System | Debian 13.6 |
| IP Address | `192.168.50.201` |
| CPU | 1 core |
| RAM | 256 MB |
| Disk | 4 GB |
| Web Server | NGINX |
| Internal Protocol | HTTP |
| Internal Port | 80 |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/containers.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

Public Endpoints provides:

- Public static file hosting
- Third-party verification endpoints
- Internet-facing HTTPS resources

The service avoids exposing internal applications directly to the internet.

Currently hosted:

- Tesla Fleet API public key

---

# Architecture

```text
Internet
    |
    v
Cloudflare
    |
    v
NGINX Proxy Manager
(LXC 102)
192.168.50.87
    |
    v
public-endpoints
(LXC 105)
192.168.50.201
    |
    v
Static Verification Files
```

TLS termination is handled by NGINX Proxy Manager.

Internal services such as Home Assistant are not publicly exposed.

---

# Network Configuration

Verified address:

| Interface | Address | Purpose |
|-----------|---------|---------|
| `eth0` | `192.168.50.201/24` | Main LAN |

The container receives its address through DHCP.

---

# Web Server

Verified:

```text
nginx.service
active (running)
```

Listening port:

```text
HTTP :80
```

---

# Directory Structure

```text
/var/www/html/
├── index.html
└── .well-known/
    └── appspecific/
        └── com.tesla.3p.public-key.pem
```

Private key storage:

```text
/etc/public-endpoints/
└── keys/
    └── private-key.pem
```

The private key is stored outside the web root.

It must never be committed to Git or publicly exposed.

---

# Tesla Fleet Public Key

Public URL:

```text
https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Public file:

```text
/var/www/html/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Private key:

```text
/etc/public-endpoints/keys/private-key.pem
```

---

# NGINX Proxy Manager

Verified proxy configuration:

| Setting | Value |
|-----------|-------|
| Domain | `tesla.phanom-lab.org` |
| Scheme | HTTP |
| Forward Host | `192.168.50.201` |
| Forward Port | `80` |
| Force SSL | Enabled |
| HSTS | Enabled |

---

# Cloudflare

The DNS record is proxied through Cloudflare.

Verified:

- Public DNS resolution
- Cloudflare proxy
- HTTPS access

Cloudflare provides:

- Public DNS
- TLS proxy
- DDoS protection
- HTTPS availability

---

# Verification

Internal:

```bash
curl http://192.168.50.201
```

Public:

```bash
curl https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Expected:

```text
-----BEGIN PUBLIC KEY-----
...
-----END PUBLIC KEY-----
```

Verified:

```text
HTTP/2 200
server: cloudflare
```

---

# Security

- Static content only
- No PHP
- No database
- No public management interface
- Home Assistant remains private
- Private key stored outside web root
- HTTPS terminated by NGINX Proxy Manager
- Cloudflare proxy enabled

---

# Backup

Important data:

```text
/var/www/html/
/etc/public-endpoints/
/etc/nginx/
```

The private key should exist in encrypted offline backups.

---

# Restore Procedure

1. Restore or recreate LXC 105.
2. Install NGINX.
3. Restore `/var/www/html`.
4. Restore `/etc/public-endpoints`.
5. Verify private key permissions.
6. Restore NGINX configuration.
7. Restore NGINX Proxy Manager proxy host.
8. Verify HTTPS access.

---

# Future Improvements

- Configure static IP instead of DHCP reservation.
- Add monitoring and health checks.
- Support additional public verification endpoints when required.

---

# Related Documentation

- `docs/architecture.md`
- `docs/security.md`
- `docs/network/vlans.md`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
