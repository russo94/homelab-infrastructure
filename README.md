# Homelab Infrastructure

A production-oriented homelab built on Proxmox VE, focused on security, reliability, and maintainability.

This repository is the **single source of truth** for the infrastructure, documenting the architecture, networking, security, deployed services, operational procedures, and inventory.

---

# Goals

- Build a secure, reliable, and maintainable self-hosted environment.
- Document every infrastructure change.
- Track all changes using Git.
- Prefer industry best practices over quick fixes.
- Design for scalability and long-term maintainability.
- Maintain a single source of truth for all documentation.

---

# Current Infrastructure

| Service | Status |
|---------|--------|
| Pi-hole | ✅ Production |
| Vaultwarden | ✅ Production |
| NGINX Proxy Manager | ✅ Production |
| Tailscale Gateway | ✅ Production |
| Public Endpoints | ✅ Production |
| Home Assistant | 🚧 Planned |

---

# Repository Structure

```text
homelab-infrastructure/
│
├── README.md
│
├── docs/
│   ├── architecture.md
│   ├── security.md
│   │
│   ├── network/
│   │   ├── README.md
│   │   ├── vlans.md
│   │   ├── firewall.md
│   │   ├── dns.md
│   │   ├── dhcp.md
│   │   └── routing.md
│   │
│   ├── services/
│   │   ├── public-endpoints.md
│   │   └── tailscale-gateway.md
│   │
│   ├── integrations/
│   │   └── tesla-fleet.md
│   │
│   └── adr/
│       └── ADR-001-public-endpoints.md
│
├── inventory/
│   ├── containers.md
│   ├── ip-addresses.md
│   └── virtual-machines.md
│
└── diagrams/
```

---

# Documentation

## Architecture

High-level design of the homelab, including infrastructure layout, networking strategy, and system relationships.

---

## Network

The network documentation is divided into dedicated documents:

- Overview
- VLANs
- Firewall policy
- DNS architecture
- DHCP architecture
- Routing

---

## Security

Security policies and hardening decisions including:

- Remote access
- SSH hardening
- Authentication
- Secrets management
- Security principles

---

## Inventory

The inventory contains the current deployment state.

It is the authoritative source for:

- Virtual machines
- Linux containers
- IP address assignments

---

## Services

Each service has its own documentation describing:

- Purpose
- Dependencies
- Configuration
- Operational notes

Deployment-specific information such as IP addresses and resource allocations is referenced from the inventory rather than duplicated.

---

## Integrations

Third-party integrations with external systems.

---

## Architecture Decision Records (ADR)

Important architectural decisions are documented as ADRs to explain why significant design choices were made.

---

# Documentation Principles

This repository follows several documentation principles.

## Single Source of Truth

Every piece of information should exist in only one location.

Other documents reference the canonical source instead of duplicating information.

---

## Separation of Concerns

Each document has a clearly defined responsibility.

Examples:

- Architecture explains **how the system is designed**.
- Inventory describes **what is currently deployed**.
- Service documents describe **individual services**.
- Network documents describe **network architecture**.

---

## Document Facts, Not Assumptions

Whenever possible, documentation should describe verified facts.

Design decisions are documented separately from implementation details.

Assumptions should be verified before being documented as facts.

---

# Infrastructure Workflow

Every infrastructure change follows the same lifecycle:

1. Design
2. Implement
3. Verify
4. Document
5. Commit
6. Push

The repository should always accurately represent the production environment.

---

# Future Documentation

Planned additions include:

- Disaster Recovery
- Operational Procedures
- Hardware Inventory
- Storage Inventory
- Service Runbooks
- Infrastructure Diagrams

---

# License

This repository is intended for personal infrastructure documentation.
