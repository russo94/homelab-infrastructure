# ADR-001: Use a Dedicated Public Endpoints Service

**Status:** Accepted

**Date:** 2026-07-23

---

# Context

The Tesla Fleet API requires a publicly accessible HTTPS endpoint that serves a developer public key.

Several implementation options were considered:

1. Expose Home Assistant directly.
2. Serve the public key from Home Assistant.
3. Deploy a dedicated web server for public verification files.

The homelab design prioritizes minimizing the public attack surface while keeping internal services isolated.

---

# Decision

A dedicated Debian LXC container (`public-endpoints`, CT105) will host all publicly accessible static verification files.

Traffic flows as follows:

```
Internet
    │
Cloudflare
    │
NGINX Proxy Manager
    │
public-endpoints
```

Home Assistant remains accessible only through Tailscale and is never exposed to the Internet.

---

# Rationale

This approach provides several advantages:

- Home Assistant remains private.
- Reduced attack surface.
- Easier auditing of public services.
- Static content only.
- Independent lifecycle from Home Assistant.
- Simple disaster recovery.
- Future public verification services can reuse the same container.

---

# Consequences

## Positive

- Strong separation of responsibilities.
- Easier maintenance.
- Better security posture.
- Easier to rebuild independently.
- Scales to additional public endpoints.

## Negative

- Additional LXC container to maintain.
- Slightly more infrastructure complexity.

---

# Alternatives Considered

## Expose Home Assistant

Rejected.

Reason:

Unnecessarily increases the attack surface of a critical internal service.

---

## Serve files from Home Assistant

Rejected.

Reason:

Mixes public infrastructure with internal application responsibilities.

---

## Host files directly from NGINX Proxy Manager

Rejected.

Reason:

Possible, but mixes reverse proxy configuration with application data and complicates backups and future expansion.

---

# Security Considerations

The dedicated service:

- hosts only static files;
- contains no application runtime;
- stores private keys outside the web root;
- is protected by Cloudflare and NGINX Proxy Manager;
- can be restored independently.

---

# Review

This decision should be revisited if:

- Tesla Fleet API requirements change;
- a centralized public web service is introduced;
- infrastructure is migrated away from Proxmox.
