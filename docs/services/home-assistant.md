# Home Assistant

## Purpose

Home Assistant is the central home automation platform for the homelab.

It integrates smart devices, automations, sensors, and dashboards into a single management interface.

---

# Role in the Homelab

Home Assistant provides centralized automation and monitoring for the home environment.

Typical responsibilities include:

- Device integration
- Automations
- Dashboards
- Notifications
- Presence detection
- Energy monitoring
- Smart home management

---

# Deployment

| Property | Value |
|----------|-------|
| Type | LXC |
| Host | Proxmox VE |
| Status | Production |
| Operating System | Debian |
| Inventory | See `inventory/containers.md` |

Deployment-specific information such as container ID, CPU, memory, and IP address is maintained in the inventory.

---

# Network

Home Assistant is deployed on the Main LAN.

Access is limited to trusted internal networks unless explicitly published.

IP addressing is documented in:

`inventory/ip-addresses.md`

---

# Dependencies

Home Assistant depends on:

- Proxmox VE
- Router
- DNS
- Network connectivity

Additional integrations may introduce further dependencies.

---

# Dependents

The following rely on Home Assistant:

- Home automations
- Smart devices
- Dashboards
- Mobile application
- Notifications

---

# Integrations

Installed integrations should be documented separately under:

`docs/integrations/`

Each integration should describe:

- Purpose
- Dependencies
- Configuration
- Restore considerations

---

# Data

Important data includes:

- Configuration
- Automations
- Dashboards
- Integrations
- Add-ons
- Secrets
- User configuration

Persistent data must always be included in backups.

---

# Backup

Home Assistant is included in the homelab backup strategy.

Backup implementation is documented in the `offsite-backup-v2` repository.

---

# Restore

General recovery order is documented in:

`docs/disaster-recovery.md`

After restoring Home Assistant, verify:

- Web interface
- Automations
- Integrations
- Dashboards
- Mobile application
- Notifications

---

# Updates

Update during scheduled maintenance.

After updating, verify:

- Startup completed successfully
- Automations execute correctly
- Integrations reconnect
- Dashboards load
- Logs contain no critical errors

---

# Monitoring

Routine health checks include:

- Container running
- Web interface accessible
- Automations functioning
- Integrations online
- System logs clean

---

# Troubleshooting

Common checks include:

- Verify the container is running.
- Review Home Assistant logs.
- Confirm integrations are connected.
- Verify network connectivity.
- Check automation traces.
- Test dashboard accessibility.

---

# Related Documentation

- `docs/architecture.md`
- `docs/disaster-recovery.md`
- `docs/network/`
- `docs/integrations/`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
