# Pi-hole

## Purpose

Pi-hole provides network-wide DNS filtering for the homelab.

It blocks advertisements, trackers, and malicious domains while acting as the primary DNS resolver for supported networks.

---

# Role in the Homelab

Pi-hole is one of the core infrastructure services.

It provides:

- Network-wide DNS filtering
- Local DNS resolution
- Centralized DNS management
- Improved privacy
- Reduced unwanted network traffic

Loss of Pi-hole affects DNS resolution for networks that depend on it.

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

Pi-hole is deployed on the Main LAN.

It provides DNS services for:

- Main LAN
- VLAN 10 (Personal)

The router uses Pi-hole as its default upstream DNS server.

Some isolated VLANs override DNS to use public resolvers instead of Pi-hole.

IP addressing is documented in:

`inventory/ip-addresses.md`

---

# Dependencies

Pi-hole depends on:

- Proxmox VE
- Network connectivity
- Router
- Internet connectivity

---

# Dependents

The following infrastructure depends on Pi-hole:

- Main LAN clients
- VLAN 10 clients
- Router DNS configuration

Additional services may rely on Pi-hole for DNS resolution.

---

# Data

Important data includes:

- DNS configuration
- Blocklists
- Local DNS records
- Group assignments
- Client configuration

Persistent configuration should be included in backups.

---

# Backup

Pi-hole is included in the homelab backup strategy.

Backup implementation is documented in the `offsite-backup-v2` repository.

---

# Restore

General recovery order is documented in:

`docs/disaster-recovery.md`

After restoring Pi-hole, verify:

- DNS resolution
- Blocklists
- Local DNS records
- Client queries
- Router DNS configuration

---

# Updates

Update Pi-hole during planned maintenance.

After updating, verify:

- DNS resolution
- Admin web interface
- Blocklists
- Query logging

---

# Monitoring

Routine health checks include:

- Admin dashboard accessible
- DNS queries resolving correctly
- Blocklists updated
- Container running
- No critical log errors

---

# Troubleshooting

Common checks include:

- Verify the container is running.
- Verify DNS port 53 is reachable.
- Confirm the router is using Pi-hole as its DNS server.
- Check Pi-hole logs.
- Test DNS resolution from a client.

---

# Related Documentation

- `docs/architecture.md`
- `docs/network/`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
