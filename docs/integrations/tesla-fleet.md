# Tesla Fleet Integration

## Purpose

This document describes the integration between Home Assistant and the Tesla Fleet API.

The Tesla Fleet API requires a publicly accessible HTTPS endpoint that hosts a developer public key. Rather than exposing Home Assistant directly to the Internet, a dedicated service (`public-endpoints`) is used.

---

# Objectives

- Keep Home Assistant private.
- Minimize the public attack surface.
- Meet Tesla Fleet API requirements.
- Allow the public endpoint to be rebuilt independently.

---

# Architecture

```
Tesla Fleet API
        │
        ▼
Cloudflare
        │
        ▼
NGINX Proxy Manager
        │
        ▼
public-endpoints
(LXC 105)
        │
        ▼
Tesla Public Key

----------------------------

Home Assistant
(VM 103)
        │
        ▼
Tailscale
```

Home Assistant is **never directly reachable from the Internet**.

---

# Components

| Component | Purpose |
|-----------|---------|
| Cloudflare | Public DNS and reverse proxy |
| NGINX Proxy Manager | TLS termination and reverse proxy |
| public-endpoints | Hosts static verification files |
| Home Assistant | Local automation platform |
| Tailscale | Secure remote administration |

---

# Tesla Key Pair

Private key:

```
/etc/public-endpoints/keys/private-key.pem
```

Public key:

```
/var/www/html/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Public endpoint:

```
https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

The private key must never leave the server except as part of an encrypted backup.

---

# Security Design

The public endpoint exposes only:

```
/.well-known/appspecific/com.tesla.3p.public-key.pem
```

No Home Assistant endpoints are published.

No Home Assistant ports are forwarded.

No Tesla traffic reaches Home Assistant directly.

---

# Verification

Internal test:

```bash
curl http://192.168.50.201/.well-known/appspecific/com.tesla.3p.public-key.pem
```

External test:

```bash
curl https://tesla.phanom-lab.org/.well-known/appspecific/com.tesla.3p.public-key.pem
```

Expected result:

```
-----BEGIN PUBLIC KEY-----
...
-----END PUBLIC KEY-----
```

---

# Recovery Procedure

If the container is lost:

1. Restore LXC 105.
2. Restore the Tesla private key.
3. Regenerate the public key if required.
4. Verify file permissions.
5. Restore the NGINX Proxy Manager proxy host.
6. Confirm public HTTPS access.

If the private key is lost, a new Tesla key pair must be generated and the Tesla Developer Portal configuration updated.

---

# Future Improvements

- Add automated health monitoring.
- Add configuration management using Ansible.
- Support additional public verification endpoints if required.
