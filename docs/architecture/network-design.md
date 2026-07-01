# Network Design — BrightBuild Construction Pty Ltd

**Document:** Network Design v1.0
**Sprint:** Sprint 0 — Project Initiation
**Status:** Approved

---

## Network Diagram

```
                        Internet
                           |
                    Cloudflare DNS
                    (brightbuild.com.au)
                           |
                   Business Firewall
                   (pfSense / similar)
                           |
                      Core Switch
                     (VLAN-aware)
                    /             \
          VLAN 10 (Servers)    VLAN 20 (Clients)
          10.10.10.0/24        10.10.20.0/24
               |                     |
        ┌──────┴──────┐         Workstations
        |             |         (DHCP from DC01)
   BRIS-HO-DC01  BRIS-HO-FS01
   10.10.10.10   10.10.10.11
   AD/DNS/DHCP   Files/Print
        |
        |        Microsoft 365
        |        Exchange Online
        |        Teams / SharePoint
        |        Entra ID
        |
        |        Azure
                 Azure VM (future)
                 Azure Backup
                 Azure VPN Gateway

                       |
              [VPN Tunnel — IPSec]
                       |
              Gold Coast Branch
              10.20.10.0/24
              (7 staff, local switch)

              Remote Workers (5)
              VPN Client → 10.99.0.0/24
```

---

## Traffic Flow

**Internal user accessing file server:**
```
Client PC → Core Switch (VLAN 20) → Firewall → Core Switch (VLAN 10) → BRIS-HO-FS01
```

**User accessing email:**
```
Client PC → Firewall → Internet → Microsoft 365 Exchange Online
```

**Gold Coast staff accessing Brisbane file server:**
```
GC Workstation → GC Firewall → IPSec VPN Tunnel → Brisbane Firewall → BRIS-HO-FS01
```

**Remote worker accessing company resources:**
```
Laptop → VPN Client (SSL/IKEv2) → Brisbane Firewall → Internal network
```

---

## Firewall Rules (Summary)

| Rule | Source | Destination | Action |
|------|--------|-------------|--------|
| Clients → Internet | VLAN 20 | Any | Allow |
| Clients → Servers | VLAN 20 | VLAN 10 | Allow (specific ports only) |
| Servers → Internet | VLAN 10 | Any | Allow (Windows Update, M365) |
| VPN → Internal | 10.99.0.0/24 | 10.10.0.0/16 | Allow |
| Site-to-Site | 10.20.0.0/16 | 10.10.0.0/16 | Allow |
| All else | Any | Any | Deny (default) |

---

## External DNS (Cloudflare)

| Record | Type | Value |
|--------|------|-------|
| brightbuild.com.au | MX | Microsoft 365 |
| brightbuild.com.au | TXT | SPF record |
| autodiscover | CNAME | Microsoft 365 |
| vpn.brightbuild.com.au | A | Brisbane Firewall public IP |

---

## Key Design Decisions

**Why separate VLANs for servers and clients?**
A staff laptop getting a virus should not be able to directly scan and attack the domain controller. VLAN separation + firewall rules limit the blast radius.

**Why Cloudflare for public DNS?**
Already familiar with it, DDoS protection built in, fast propagation. Internal DNS (brightbuild.local) is handled by the Domain Controller.

**Why not put everything in Azure first?**
Real SMBs in Australia still run on-premise Windows Server + AD as the core, then extend to cloud. We're building it the way it exists in the real world, not the way Microsoft wants you to buy licences.
