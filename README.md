# Homelab Infrastructure

A production-oriented homelab built on Proxmox VE, focused on security, reliability, and maintainability.

This repository serves as the single source of truth for the infrastructure, documenting architecture, networking, security, services, and operational procedures.

---

## Goals

- Build a secure and reliable self-hosted environment.
- Document every infrastructure change.
- Use Git for version control and change tracking.
- Prefer industry best practices over quick fixes.
- Keep the infrastructure modular and easy to expand.

---

## Current Infrastructure

| Service | Status |
|---------|--------|
| Tailscale Gateway | ✅ Production |
| Pi-hole | ✅ Running |
| Vaultwarden | ✅ Running |
| NGINX Proxy Manager | ✅ Running |
| Home Assistant | 🚧 Planned |

---

## Repository Structure

```text
homelab-infrastructure/
│
├── README.md
├── docs/
│   ├── architecture.md
│   ├── network.md
│   ├── security.md
│   └── services/
│
├── inventory/
│
└── diagrams/
```

---

## Documentation

- **Architecture** – Overall homelab design and infrastructure decisions.
- **Network** – Network layout, VLANs, IP addressing, and connectivity.
- **Security** – SSH hardening, authentication, and security practices.
- **Services** – Documentation for each deployed service.
- **Inventory** – Virtual machines, containers, and IP address assignments.

---

## Workflow

Every infrastructure change follows the same lifecycle:

1. Design
2. Build
3. Verify
4. Document
5. Commit

This ensures the repository always reflects the current production environment.

---

## Principles

- Infrastructure as Documentation
- Security First
- Keep It Simple
- No undocumented changes
- Production before convenience

---

## License

This repository is intended for personal infrastructure documentation.
