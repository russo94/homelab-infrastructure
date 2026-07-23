## Router Default DNS

The ASUS GT-BE98 router is configured with the following default upstream DNS server:

| Setting | Value |
|---------|-------|
| Default DNS | `192.168.50.52` (Pi-hole) |

Networks that do not specify their own DNS server inherit this default.

---

## VLAN DNS Policy

| Network | DNS Configuration | Reason |
|---------|-------------------|--------|
| Main LAN | Router default (Pi-hole) | Infrastructure DNS |
| VLAN 10 | Router default (Pi-hole) | Trusted devices |
| VLAN 20 | Override to `1.1.1.1` | Independent of infrastructure DNS |
| VLAN 30 | Override to `1.1.1.1` | Independent of infrastructure DNS |
| VLAN 40 | Override to `1.1.1.1` | Independent of infrastructure DNS |
| VLAN 60 | Router default | Guest network uses the router's default DNS configuration |

---

## Pi-hole

Pi-hole provides:

- DNS filtering
- Advertisement blocking
- Local DNS resolution
- Centralized DNS management

Pi-hole is used by trusted networks through the router's default DNS configuration.

---

## Design Rationale

The default router DNS points to Pi-hole to provide centralized DNS for trusted infrastructure.

Networks that are intentionally isolated from the Main LAN (VLANs 20, 30, and 40) override the default DNS with `1.1.1.1` to avoid depending on infrastructure services that are outside their trust boundary.

VLAN 60 currently inherits the router's default DNS configuration. The exact DNS forwarding behavior of the ASUS router should be verified and documented separately.
