# Changelog

All notable changes to this project are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

---

## [0.1.0] - 2026-07-02
### Sprint 0 — Project Initiation

### Added
- Repository structure: `docs/`, `labs/`, `scripts/`, `tickets/`, `portfolio/`, `screenshots/`, `interview-notes/`, `assets/`
- `docs/architecture/enterprise-overview.md` — company profile, IT stack, departments, business requirements
- `docs/architecture/network-design.md` — topology diagram, traffic flows, firewall rules, external DNS
- `docs/architecture/naming-convention.md` — server, workstation, user, group, and share naming standards
- `docs/architecture/ip-address-plan.md` — subnet design, DHCP scope, DNS configuration, IP assignments
- `docs/architecture/active-directory-design.md` — OU structure, GPOs, user template, drive mapping, Sprint 1 lab targets
- Virtual client defined: **BrightBuild Construction Pty Ltd** (35 staff, Brisbane HQ + Gold Coast branch)

### Fixed
- Domain name: `brightbuild.local` → `ad.brightbuild.com.au`
  - `.local` conflicts with mDNS, blocks certificate issuance, complicates Entra ID sync

### Changed
- OU structure: location-based (Brisbane/GoldCoast) → department-based (Finance/HR/Management/IT/Operations)
  - GPOs follow department logic, not geography. Location stored as user attribute.
- Password policy: 90-day expiry removed → no expiry + MFA + Conditional Access + Entra ID Protection
  - Microsoft deprecated periodic rotation in 2019. Modern Identity replaces it.
- Windows Update: WSUS removed → Windows Update for Business (GPO-managed, no server required)
  - WSUS is unnecessary overhead for 35 users. Intune to be introduced in Phase 2.
- Server role labels: "File Server / Print Server" → "File Services / Print Services"
  - Documents services, not hardware. Implementation may change (VM, container, cloud).
- DNS forwarder: `8.8.8.8` removed → Firewall / `1.1.1.1` (TBD — DNS Design session pending)
  - Google DNS not appropriate for enterprise (privacy, logging).
- VPN references: generic "VPN" → explicit type labels
  - Site-to-site (Brisbane ↔ Gold Coast): IPSec / WireGuard — TBD
  - Remote Access (remote workers): SSL VPN / WireGuard / IKEv2 — TBD

### Decisions
- **ADR-0001:** All designs must satisfy Enterprise Standard → MSP Reality → SMB Budget. Not Microsoft's luxury solution — what a real Brisbane MSP deploys for 30–100 person clients.
- **ADR-0002:** Optimise for employability, not knowledge. Only learn what a Junior MSP Engineer in Brisbane encounters in their first 6 months.

### Added (continued)
- `PROGRESS.md` — skill readiness dashboard with defined level criteria (0/25/50/75/100%) and Brisbane MSP job frequency weighting

### Deferred
- DNS Design session (forwarder selection, split DNS, conditional forwarders)
- VPN Design session (protocol selection for site-to-site and remote access)
