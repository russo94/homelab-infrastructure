# Pi-hole

## Purpose

Pi-hole provides DNS filtering and DNS resolution services for the homelab.

It is a core infrastructure service responsible for:

- DNS filtering
- Local DNS resolution
- Query visibility
- Network-wide blocking

---

# Deployment

| Property | Value |
|----------|-------|
| Type | LXC Container |
| Container ID | `100` |
| Hostname | `pihole` |
| IP Address | `192.168.50.52` |
| Network | Main LAN |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/containers.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

Pi-hole provides DNS services for trusted devices.

The service runs inside an isolated LXC container while remaining part of the infrastructure network.

Current responsibilities:

- DNS filtering
- DNS forwarding
- Local DNS handling
- Query logging

---

# Network Configuration

Pi-hole is reachable at:

```text
192.168.50.52:53
```

DNS is provided using:

- UDP port 53
- TCP port 53

Verified listener:

```text
0.0.0.0:53
[::]:53
```

---

# DNS Architecture

The current DNS flow is:

```
Client Device
      |
      |
      v
Pi-hole FTL
      |
      |
      v
Unbound
127.0.0.1:5335
      |
      |
      v
DNS Resolution
```

Pi-hole forwards DNS requests internally to Unbound.

Verified configuration:

```text
server=127.0.0.1#5335
```

---

# VLAN DNS Design

The router provides DNS configuration per network.

Current design:

| Network | DNS Configuration |
|----------|------------------|
| Main LAN | Pi-hole (`192.168.50.52`) |
| VLAN 10 Personal Devices | Pi-hole (`192.168.50.52`) |
| VLAN 20 IoT | `1.1.1.1` |
| VLAN 30 Media Devices | `1.1.1.1` |
| VLAN 40 Cameras | `1.1.1.1` |
| VLAN 60 Guest Network | Restricted network DNS configuration |

Some VLANs intentionally bypass Pi-hole to avoid communication from isolated networks to infrastructure services.

Detailed VLAN policy:

`docs/network/`

---

# Dependencies

Pi-hole depends on:

- Proxmox VE
- Network availability
- Router configuration
- VLAN routing rules
- Unbound DNS resolver

---

# Dependents

The following systems depend on Pi-hole:

- Main LAN devices
- VLAN 10 personal devices
- Infrastructure DNS resolution

---

# Persistent Data

Important Pi-hole data includes:

- DNS configuration
- Blocklists
- Local DNS records
- Query database
- Client configuration

Persistent data must be included in backups.

---

# Backup

Backup strategy:

`offsite-backup-v2`

Pi-hole container recovery should restore:

- Container state
- Configuration
- DNS settings
- Custom records

---

# Restore Procedure

General recovery order:

`docs/disaster-recovery.md`

After restoring Pi-hole:

1. Start the container.
2. Verify IP address.
3. Verify Pi-hole service status.
4. Verify DNS port availability.
5. Verify client DNS resolution.

---

# Verification

Last verified:

2026-07-23

Checks performed:

## Container Network

Command:

```bash
pct exec 100 -- ip addr
```

Result:

```text
192.168.50.52/24
```

---

## Service Status

Command:

```bash
pct exec 100 -- systemctl status pihole-FTL
```

Result:

```text
Active: active (running)
```

---

## DNS Listener

Command:

```bash
pct exec 100 -- ss -tulpn | grep :53
```

Result:

```text
DNS listening on port 53
```

---

## DNS Resolution Test

Command:

```bash
nslookup google.com 192.168.50.52
```

Result:

```text
DNS resolution successful
```

---

# Troubleshooting

## Check container status

```bash
pct status 100
```

---

## Check Pi-hole service

```bash
pct exec 100 -- systemctl status pihole-FTL
```

---

## Check DNS listener

```bash
pct exec 100 -- ss -tulpn | grep :53
```

---

## Test DNS resolution

```bash
nslookup example.com 192.168.50.52
```

---

# Related Documentation

- `docs/network/`
- `docs/disaster-recovery.md`
- `inventory/containers.md`
- `inventory/ip-addresses.md`
