# Public Endpoints

## Purpose

`public-endpoints` is a minimal, dedicated web service that hosts static files requiring public HTTPS access.

Its primary purpose is to satisfy third-party verification requirements without exposing internal services, such as Home Assistant, directly to the Internet.

The service currently hosts the Tesla Fleet API public key.

---

# Service Information

| Property | Value |
|-----------|-------|
| Type | LXC Container |
| Container ID | 105 |
| Hostname | public-endpoints |
| Operating System | Debian 13 |
| IP Address | 192.168.50.201 |
| Web Server | NGINX |
| Internal Protocol | HTTP |
| Internal Port | 80 |
| Public Hostname | tesla.phanom-lab.org |
| Public Protocol | HTTPS |

---

# Architecture

```
Internet
    │
    ▼
Cloudflare
    │
    ▼
NGINX Proxy Manager
(LXC 102)
192.168.50.87
    │
    ▼
public-endpoints
(LXC 105)
192.168.50.201
    │
    ▼
Static Verification Files
```

TLS termination is handled by NGINX Proxy Manager using the existing wildcard certificate.

Home Assistant is **not** publicly exposed.

---

# Directory Structure

```
/var/www/html/
├── index.html
└── .well-known/
    └── appspecific/
        └── com.tesla.3p.public-key.pem

/etc/public-endpoints/
└── keys/
    └── private-key.pem
```

---

# Tesla Fleet Public Key

Public URL

```
https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Public file

```
/var/www/html/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Private key

```
/etc/public-endpoints/keys/private-key.pem
```

The private key **must never** be stored inside the web root or committed to Git.

---

# NGINX Proxy Manager

| Setting | Value |
|-----------|-------|
| Domain | tesla.phanom-lab.org |
| Scheme | HTTP |
| Forward IP | 192.168.50.201 |
| Forward Port | 80 |
| Block Common Exploits | Enabled |
| Force SSL | Enabled |
| HTTP/2 | Enabled |
| HSTS | Enabled |

---

# Cloudflare

The DNS record for `tesla.phanom-lab.org` is proxied through Cloudflare.

Cloudflare provides:

- Public DNS
- TLS proxy
- DDoS protection
- HTTPS access

---

# Verification

Internal

```bash
curl http://192.168.50.201
```

Public

```bash
curl https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Expected result

```
-----BEGIN PUBLIC KEY-----
...
-----END PUBLIC KEY-----
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

The following must be backed up:

```
/etc/public-endpoints/
/var/www/html/
/etc/nginx/
```

The Tesla private key should also exist in an encrypted offline backup.

---

# Restore Procedure

1. Restore or recreate LXC 105.
2. Install NGINX.
3. Restore `/var/www/html`.
4. Restore `/etc/public-endpoints`.
5. Verify private key permissions.
6. Verify the public key endpoint.
7. Restore the NGINX Proxy Manager proxy host.
8. Verify HTTPS access.

---

# Future Improvements

- Configure static IP inside the container instead of relying on DHCP reservation.
- Add monitoring and health checks.
- Support additional public verification endpoints when required.
