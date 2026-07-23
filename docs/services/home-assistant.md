# Home Assistant

## Purpose

Home Assistant is the central home automation platform for the homelab.

It integrates smart devices, automations, sensors, dashboards, and notifications into a single management interface.

---

# Deployment

| Property | Value |
|----------|-------|
| Type | Virtual Machine |
| VM ID | `103` |
| Hostname | `homeassistant` |
| Operating System | Home Assistant OS 18.1 |
| Home Assistant Core | `2026.7.3` |
| Supervisor | `2026.07.3` |
| Architecture | amd64 |
| Machine Type | `q35` |
| CPU | 2 cores |
| RAM | 4096 MB |
| Disk | 32 GB |
| Network Adapter | VirtIO |
| Bridge | `vmbr0` |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/virtual-machines.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

Home Assistant provides:

- Smart home automation
- Device integration
- Dashboards
- Notifications
- Presence detection
- Energy monitoring
- Home environment monitoring

It acts as the central automation platform for connected devices.

---

# Network Configuration

Verified network address:

| Interface | Address | Purpose |
|-----------|---------|---------|
| `enp6s18` | `192.168.50.194/24` | Main LAN |

Home Assistant internal networking:

| Interface | Address | Purpose |
|-----------|---------|---------|
| `docker0` | `172.30.232.1` | Container networking |
| `hassio` | `172.30.32.1` | Supervisor networking |

The Home Assistant web interface is available on:

```text
http://192.168.50.194:8123
```

---

# Architecture

Home Assistant runs as a dedicated virtual machine.

Architecture:

```text
Proxmox VE
 |
 └── VM 103
       |
       └── Home Assistant OS
              |
              ├── Home Assistant Core
              ├── Supervisor
              └── Add-ons
```

---

# Installed Components

Verified:

- Home Assistant OS
- Home Assistant Core
- Supervisor

Current versions:

```text
Home Assistant Core:
2026.7.3

Supervisor:
2026.07.3
```

---

# Dependencies

Home Assistant depends on:

- Proxmox VE
- Network availability
- DNS resolution
- Internet connectivity
- Connected smart devices and integrations

---

# Data

Important Home Assistant data includes:

- Configuration
- Automations
- Dashboards
- Integrations
- Add-on configuration
- Secrets
- User configuration

Persistent data must be included in backups.

---

# Backup

Home Assistant should be included in the regular Proxmox backup strategy.

Backup implementation is documented in the separate:

```text
offsite-backup-v2
```

repository.

---

# Restore

General recovery order:

`docs/disaster-recovery.md`

After restoring:

1. Start VM 103.
2. Verify network connectivity.
3. Verify Home Assistant availability.
4. Verify automations.
5. Verify integrations.
6. Verify dashboards.

---

# Monitoring

Routine checks:

- VM running
- Home Assistant web interface accessible
- Supervisor healthy
- Integrations online
- Automations functioning

Verified:

```text
Supervisor health:
healthy
```

---

# Troubleshooting

Check VM state from the Proxmox host:

```bash
qm status 103
```

Check Home Assistant information from the Home Assistant OS terminal:

```bash
ha info
```

Check Supervisor from the Home Assistant OS terminal:

```bash
ha supervisor info
```

Check web availability from the Proxmox host:

```bash
curl http://192.168.50.194:8123
```

---

# Related Documentation

- `docs/architecture.md`
- `docs/network/vlans.md`
- `docs/security.md`
- `docs/disaster-recovery.md`
- `inventory/virtual-machines.md`
- `inventory/ip-addresses.md`
