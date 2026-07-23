# DNS

## Router Default DNS

The ASUS GT-BE98 router is configured with the following default upstream DNS server:

| Setting | Value |
|---------|-------|
| Default DNS | `192.168.50.52` (Pi-hole) |

Networks that do not specify their own DNS configuration inherit this default.

---

## VLAN DNS Policy

| Network | DNS Configuration | Reason |
|---------|-------------------|--------|
| Main LAN | Router default (Pi-hole) | Infrastructure DNS |
| VLAN 10 | Router default (Pi-hole) | Trusted devices |
| VLAN 20 | Configuration not verified | IoT network |
| VLAN 30 | Configuration not verified | Media devices |
| VLAN 40 | Configuration not verified | Camera network |
| VLAN 60 | Router default (Pi-hole) | Guest network |

---

## Pi-hole

Pi-hole provides:

- DNS filtering
- Advertisement blocking
- Local DNS resolution
- Centralized DNS management

Pi-hole is used by trusted networks and the guest network through the router's default DNS configuration.

---

## Design Rationale

The default router DNS points to Pi-hole to provide centralized DNS management for infrastructure and trusted networks.

Networks with reduced trust levels should have DNS behavior documented according to their actual router configuration.

DNS behavior should be verified whenever VLAN firewall or router configuration changes.
