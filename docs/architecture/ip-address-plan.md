# IP Address Plan — BrightBuild Construction Pty Ltd

**Document:** IP Address Plan v1.0
**Sprint:** Sprint 0 — Project Initiation
**Status:** Approved

---

## Summary

| Site | Subnet | VLAN | Gateway |
|------|--------|------|---------|
| Brisbane HQ — Servers | 10.10.10.0/24 | VLAN 10 | 10.10.10.1 |
| Brisbane HQ — Clients | 10.10.20.0/24 | VLAN 20 | 10.10.20.1 |
| Brisbane HQ — Management | 10.10.30.0/24 | VLAN 30 | 10.10.30.1 |
| Gold Coast Branch | 10.20.10.0/24 | VLAN 10 | 10.20.10.1 |
| VPN (Remote Workers) | 10.99.0.0/24 | — | 10.99.0.1 |

---

## Brisbane HQ — Server Subnet (10.10.10.0/24)

| IP Address | Hostname | Role |
|------------|----------|------|
| 10.10.10.1 | — | Gateway / Firewall |
| 10.10.10.2 | — | Core Switch (management IP) |
| 10.10.10.10 | BRIS-HO-DC01 | Domain Controller |
| 10.10.10.11 | BRIS-HO-FS01 | File Services / Print Services |
| 10.10.10.20 | NAS01 | Synology NAS |
| 10.10.10.100–199 | — | Reserved for future servers |

Static IPs only in this range. No DHCP.

---

## Brisbane HQ — Client Subnet (10.10.20.0/24)

| Range | Purpose |
|-------|---------|
| 10.10.20.1 | Gateway |
| 10.10.20.2–9 | Reserved |
| 10.10.20.100–200 | DHCP pool (workstations, laptops) |
| 10.10.20.201–210 | Printers (static) |
| 10.10.20.211–220 | Reserved for VoIP / other |

DHCP served by: BRIS-HO-DC01
DHCP scope: 10.10.20.100 – 10.10.20.200
Lease time: 8 hours

---

## Gold Coast Branch (10.20.10.0/24)

| IP Address | Role |
|------------|------|
| 10.20.10.1 | Gateway / Branch Firewall |
| 10.20.10.100–150 | DHCP pool (workstations) |

Site-to-site VPN connects Gold Coast to Brisbane HQ.
Gold Coast clients access \\BRIS-HO-FS01\ over VPN tunnel.

---

## DNS Configuration

| Server | Role | IP |
|--------|------|-----|
| BRIS-HO-DC01 | Primary DNS (internal) | 10.10.10.10 |
| Firewall / 1.1.1.1 | External forwarder (TBD) | — |

All internal clients point to 10.10.10.10 as DNS server.
Domain: ad.brightbuild.com.au (internal)
Public domain: brightbuild.com.au (Cloudflare)

> **Note:** External DNS forwarder to be confirmed during DNS Design session. Options: firewall upstream DNS, ISP DNS, or Cloudflare 1.1.1.1. Avoid Google 8.8.8.8 in enterprise environments (privacy, logging).

---

## Design Notes

- Servers and clients are on separate subnets (security + easier firewall rules)
- VLAN separation means a compromised client PC cannot directly reach servers
- All static IP assignments are documented here — never assign by memory
- Future growth: 10.10.40.0/24 available for wireless / IoT devices
