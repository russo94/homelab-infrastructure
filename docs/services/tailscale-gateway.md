# Tailscale Gateway

## Purpose

Tailscale Gateway provides secure remote access to the homelab infrastructure without exposing administrative services directly to the internet.

It acts as the remote administration entry point for accessing internal resources through the private Tailscale network.

---

# Deployment

| Property | Value |
|----------|-------|
| Type | Virtual Machine |
| VM ID | `104` |
| Hostname | `ts-gateway-01` |
| Operating System | Debian 13.6 |
| Firmware | OVMF (UEFI) |
| Machine Type | `q35` |
| CPU | 1 vCPU |
| RAM | 1024 MB |
| Disk | 8 GB |
| Disk Controller | VirtIO SCSI |
| Network Adapter | VirtIO |
| Bridge | `vmbr0` |
| Firewall | Enabled |
| Status | Production |
| Hypervisor | Proxmox VE |

Inventory references:

- `inventory/virtual-machines.md`
- `inventory/ip-addresses.md`

---

# Role in the Homelab

Tailscale Gateway provides:

- Secure remote administration
- Private access to homelab resources
- Remote SSH access without public port exposure
- Tailscale network connectivity

The gateway provides a controlled access path into the homelab.

---

# Network Configuration

Verified network addresses:

| Interface | Address | Purpose |
|-----------|---------|---------|
| `ens18` | `192.168.50.193/24` | Internal LAN |
| `tailscale0` | `100.68.131.104/32` | Tailscale network |

Network architecture:

```text
Remote Device
      |
      v
Tailscale Network
      |
      v
ts-gateway-01
192.168.50.193
      |
      v
Homelab LAN
192.168.50.0/24
```

---

# Deployment Architecture

Tailscale is installed directly inside the virtual machine.

Architecture:

```text
Proxmox VE
 |
 └── VM 104
       |
       ├── ssh.service
       |
       └── tailscaled.service
```

---

# Installed Software

Verified installed services:

- Tailscale
- OpenSSH Server

---

# Tailscale Configuration

Verified service:

```text
tailscaled.service
```

Status:

```text
active (running)
```

The service is enabled and starts automatically.

Verified Tailscale address:

```text
100.68.131.104
```

---

# SSH Access

SSH provides administrative access to the VM.

Verified:

```text
ssh.service active (running)
```

SSH access from the Proxmox host requires key-based authentication.

Root SSH login was not available during verification.

---

# Dependencies

Tailscale Gateway depends on:

- Proxmox VE
- Network availability
- Internet connectivity
- Tailscale service availability

---

# Backup

The VM should be included in the regular Proxmox backup strategy.

Important recovery requirements:

- VM configuration
- Virtual disk
- Tailscale configuration and authentication data stored inside the VM

The general backup implementation is maintained in the separate:

```text
offsite-backup-v2
```

repository.

---

# Recovery Procedure

If remote access fails:

1. Verify the VM is running.
2. Verify LAN connectivity.
3. Check the Tailscale service.
4. Restart Tailscale if necessary.
5. Verify Tailscale connectivity.
6. Test SSH from an authorized device.

If the node is no longer connected to the tailnet, reauthenticate it using the Tailscale CLI.

---

# Restore Procedure

General recovery order:

`docs/disaster-recovery.md`

After restoring:

1. Start VM 104.
2. Verify network connectivity.
3. Verify SSH availability.
4. Verify Tailscale service.
5. Verify remote access.

---

# Design Decisions

Tailscale is deployed inside a dedicated VM instead of directly on the Proxmox host.

Advantages:

- Infrastructure services remain isolated.
- The hypervisor has a smaller attack surface.
- Recovery is simpler if the VM becomes unavailable.
- The gateway can be rebuilt independently.
- Future migration to a dedicated infrastructure VLAN is straightforward.

---

# Verification Status

Last verified:

2026-07-23

Verified:

- VM deployment
- VM network configuration
- LAN IP address
- Tailscale IP address
- Tailscale service running
- Tailscale connection active
- SSH service running
- SSH access from the Proxmox host requires key-based authentication

Not verified:

- MagicDNS configuration
- Guest operating system firewall state

---

# Troubleshooting

Check Tailscale:

```bash
systemctl status tailscaled
```

Restart Tailscale:

```bash
systemctl restart tailscaled
```

Check connection:

```bash
tailscale status
```

Check SSH:

```bash
systemctl status ssh
```

---

# Security Notes

Do not expose SSH directly to the internet.

Administrative access should occur through:

- Tailscale
- Internal network access
- Approved authentication methods

Never commit:

- Tailscale authentication keys
- Private keys
- Secrets

---

# Related Documentation

- `docs/architecture.md`
- `docs/network/vlans.md`
- `docs/security.md`
- `docs/disaster-recovery.md`
- `inventory/virtual-machines.md`
- `inventory/ip-addresses.md`
