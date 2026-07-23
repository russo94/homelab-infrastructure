# Security

## Overview

Security is a fundamental design principle of this homelab. Every service is deployed with the goal of minimizing unnecessary exposure while maintaining ease of administration.

---

## Remote Access

Remote administration is provided exclusively through Tailscale.

Benefits:

- End-to-end encrypted connections
- No router port forwarding
- No public SSH service
- Device-based authentication
- MagicDNS support for easy host access

---

## SSH Hardening

The Tailscale gateway is configured with OpenSSH using public-key authentication only.

Effective configuration:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Authentication uses an ED25519 SSH key.

Password authentication is disabled.

Root login is disabled.

---

## GitHub Authentication

The Proxmox host authenticates to GitHub using a dedicated ED25519 SSH key.

This key is used exclusively for repository access and is separate from the SSH keys used for server administration.

---

## Secrets Management

The following information must never be committed to Git:

- Private SSH keys
- Passwords
- API tokens
- Tailscale authentication keys
- TLS private keys
- Recovery codes
- Environment files containing secrets

Sensitive configuration should remain outside the repository whenever possible.

---

## Security Principles

The homelab follows these principles:

- Least privilege
- Defense in depth
- Secure by default
- Public-key authentication
- Minimal attack surface
- Infrastructure changes must be documented

---

## Current Security Status

| Component | Status |
|----------|--------|
| SSH Public Key Authentication | ✅ Enabled |
| Password Authentication | ✅ Disabled |
| Root SSH Login | ✅ Disabled |
| Tailscale Remote Access | ✅ Enabled |
| MagicDNS | ✅ Enabled |
| GitHub SSH Authentication | ✅ Enabled |
| Router Port Forwarding for SSH | ✅ Not Required |
