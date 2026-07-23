# Documentation Standards

## Purpose

This document defines how homelab documentation should be written, organized, and maintained.

The goal is to keep the repository accurate, easy to navigate, and useful during troubleshooting, maintenance, and disaster recovery.

---

## Primary Objective

The repository should contain everything required to:

- Understand the homelab
- Operate the infrastructure
- Troubleshoot failures
- Maintain services
- Rebuild the environment
- Restore data and services after a failure

Documentation should prioritize practical recovery value over unnecessary complexity.

---

## Single Source of Truth

Every fact should have one authoritative location.

Other documents should reference the authoritative source instead of copying the same information.

Examples:

| Information | Authoritative Location |
|-------------|------------------------|
| IP addresses | `inventory/ip-addresses.md` |
| VM resources | `inventory/virtual-machines.md` |
| LXC resources | `inventory/containers.md` |
| Hardware | `inventory/hardware.md` |
| Storage | `inventory/storage.md` |
| VLAN design | `docs/network/vlans.md` |
| Access policy | `docs/network/firewall.md` |
| Recovery order | `docs/disaster-recovery.md` |
| Backup implementation | `offsite-backup-v2` repository |

---

## Separation of Concerns

Each document should have one clear responsibility.

- Architecture documents explain how components fit together.
- Inventory documents record what is currently deployed.
- Network documents describe network design and policy.
- Service documents explain how individual services operate.
- Procedure documents contain step-by-step operational instructions.
- Disaster recovery documentation defines recovery priorities and order.
- ADRs explain why significant design decisions were made.

Information should not be duplicated across documents.

---

## Recovery First

Documentation should be written with failure recovery in mind.

Before adding information, ask:

> Would this help rebuild, restore, troubleshoot, or maintain the homelab?

Recovery-critical information should be documented clearly and kept current.

---

## Facts, Decisions, and Assumptions

Documentation should distinguish between three types of information.

---

## Verified Facts

Facts must be based on:

- Current system output
- Router configuration
- Service configuration
- Direct testing
- Physical inspection

Verified facts may be documented normally.

---

## Design Decisions

Design decisions explain why something was configured in a particular way.

Significant decisions should be recorded in an Architecture Decision Record when appropriate.

---

## Assumptions

Assumptions must not be presented as verified facts.

Unverified behavior should be:

- Tested before documentation
- Clearly marked as unverified
- Added to a verification task list

---

## Templates

Reusable documentation templates are stored in:

```text
docs/templates/
```

Current templates:

| Template | Purpose |
|----------|---------|
| `service.md` | Standard structure for service documentation |

Future templates may include:

- Procedure documentation
- ADR documentation
- Recovery procedures

---

## Service Documentation

Each service document should follow the service template.

Service documentation should cover:

- Purpose
- Role in the homelab
- Deployment
- Network access
- Dependencies
- Dependents
- Persistent data
- Backup
- Restore
- Updates
- Monitoring
- Troubleshooting
- Related documentation

Deployment-specific values such as IP addresses and resource allocations should reference the inventory.

---

## Procedure Documentation

Procedures should:

- State their purpose
- List prerequisites
- Use numbered steps
- Include verification commands
- Include rollback or recovery guidance where relevant
- Avoid relying on undocumented knowledge

Commands should be safe to copy and clearly identify where they must be executed.

---

## Links and References

Documents should use repository-relative paths where practical.

Examples:

```text
docs/network/README.md
inventory/ip-addresses.md
docs/disaster-recovery.md
```

Before deleting or moving a file, search the repository for references to its old path.

---

## Sensitive Information

The following must never be committed:

- Private keys
- Passwords
- API tokens
- Authentication keys
- Recovery codes
- TLS private keys
- Secret environment variables
- Backup encryption secrets

Public keys and non-sensitive identifiers may be documented when operationally useful.

---

## Verification

Documentation changes should be verified before committing.

Recommended checks:

```bash
git status
```

```bash
git diff
```

```bash
grep -RIn --exclude-dir=.git "old-reference" .
```

The repository should not contain:

- Broken references
- Duplicate authoritative information
- Unverified values presented as facts
- Secrets
- Outdated file paths

---

## Change Workflow

Every infrastructure change should follow:

1. Design
2. Implement
3. Verify
4. Document
5. Review
6. Commit
7. Push

The repository should represent the current production environment after every completed change.

---

## Review Schedule

Documentation should be reviewed:

- After infrastructure changes
- After service upgrades
- After restore tests
- After hardware replacement
- After network changes
- During periodic repository audits

Outdated information should be corrected when discovered.
