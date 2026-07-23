# Security

## Overview

Security is a fundamental design principle of this homelab.

Every service is deployed with the goal of minimizing unnecessary exposure while maintaining ease of administration.

---

## Remote Access

Remote administration is provided through Tailscale.

Benefits:

- End-to-end encrypted connections
- No router port forwarding
- No public SSH service
- Device-based authentication
- Private network access

The Tailscale gateway provides the controlled entry point for remote administration.

---

## SSH Hardening

The Tailscale gateway is configured with OpenSSH using public-key authentication only.

Effective configuration:

PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes

Authentication uses an ED25519 SSH key.

Password authentication is disabled.

Root login is disabled.

---

## Network Segmentation

The homelab uses VLAN separation to reduce unnecessary access between device categories.

Current segmentation:

- Main LAN for infrastructure services
- VLAN 10 for trusted personal devices
- VLAN 20 for IoT devices
- VLAN 30 for media devices
- VLAN 40 for cameras
- VLAN 60 for guest devices

Infrastructure access is controlled through network firewall policies.

---

## Public Exposure

Only explicitly approved services are exposed externally.

Current public services:

- Vaultwarden
- Tesla Fleet public endpoint

Public traffic flow:

Internet

|

Cloudflare

|

NGINX Proxy Manager

|

Internal Services

SSH is not exposed directly to the Internet.

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
| SSH Public Key Authentication | Enabled |
| Password Authentication | Disabled |
| Root SSH Login | Disabled |
| Tailscale Remote Access | Enabled |
| MagicDNS | Not verified |
| GitHub SSH Authentication | Enabled |
| Router Port Forwarding for SSH | Not Required |
| Cloudflare Proxy | Enabled |
| NGINX Proxy Manager TLS | Enabled |
| SSH Internet Exposure | Disabled |
