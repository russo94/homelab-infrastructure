# Tailscale Gateway

## Overview

The Tailscale Gateway provides secure remote administrative access to the homelab without exposing management services to the public Internet.

This virtual machine acts as the trusted entry point for remote administration.

---

## Purpose

The gateway is responsible for:

- Providing encrypted remote connectivity using Tailscale.
- Allowing SSH access from authorized devices.
- Keeping the Proxmox host isolated from direct Internet access.
- Eliminating the need for router port forwarding.

---

## Virtual Machine

| Property | Value |
|----------|-------|
| VM ID | `104` |
| Hostname | `ts-gateway-01` |
| Operating System | Debian 13.6 |
| Machine Type | q35 |
| Firmware | OVMF (UEFI) |
| CPU | 1 vCPU |
| Memory | 1 GB |
| Disk | 8 GB |
| Disk Controller | VirtIO SCSI |
| Network Adapter | VirtIO |
| Bridge | `vmbr0` |
| VLAN Tag | None |
| QEMU Guest Agent | Enabled |

---

## Network

| Property | Value |
|----------|-------|
| LAN Address | `192.168.50.193` |
| Tailscale Address | `100.68.131.104` |
| MagicDNS Hostname | `ts-gateway-01` |

---

## Installed Software

- Tailscale
- OpenSSH Server
- QEMU Guest Agent
- sudo
- curl

---

## SSH Configuration

The gateway accepts SSH connections using public-key authentication only.

Effective configuration:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Root login is disabled.

Password authentication is disabled.

Administration is performed using an ED25519 SSH key.

---

## Access Methods

### From the Local Network

```bash
ssh phanom@192.168.50.193
```

### From Anywhere

```bash
ssh phanom@ts-gateway-01
```

MagicDNS automatically resolves the hostname over the private Tailscale network.

---

## Verification

The following items were verified after deployment:

- VM boots successfully.
- QEMU Guest Agent operational.
- SSH reachable over LAN.
- SSH reachable through Tailscale.
- ED25519 authentication working.
- Password login rejected.
- Root login rejected.
- MagicDNS functioning correctly.
- GitHub SSH authentication configured on the Proxmox host.

---

## Operational Commands

### Check Tailscale Status

```bash
sudo tailscale status
```

### Display Tailscale IP

```bash
tailscale ip -4
```

### Check SSH Service

```bash
sudo systemctl status ssh
```

### Check Guest Agent

```bash
sudo systemctl status qemu-guest-agent
```

---

## Recovery Procedure

If remote access fails:

1. Verify the VM is running.
2. Verify LAN connectivity.
3. Check the Tailscale service.
4. Restart Tailscale if necessary.
5. Verify MagicDNS resolution.
6. Test SSH from another authorized device.

If the node has been removed from the tailnet, reauthenticate it using the Tailscale CLI.

---

## Design Decisions

This service exists because it offers several advantages over installing Tailscale directly on the Proxmox host:

- Infrastructure services remain isolated.
- The hypervisor has a smaller attack surface.
- Recovery is simpler if the VM becomes unavailable.
- The gateway can be rebuilt independently.
- Future migration to a dedicated infrastructure VLAN is straightforward.

---

## Status

**Production Ready**

Last verified:

- SSH Hardening ✅
- Tailscale Connected ✅
- MagicDNS Working ✅
- ED25519 Authentication ✅
- GitHub SSH Access Configured ✅
