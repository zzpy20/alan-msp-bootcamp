# Enterprise Overview — BrightBuild Construction Pty Ltd

**Document:** Enterprise Overview v1.0
**Sprint:** Sprint 0 — Project Initiation
**Status:** Draft

---

## Company Profile

| Field | Details |
|-------|---------|
| Company Name | BrightBuild Construction Pty Ltd |
| Industry | Construction |
| ABN | (simulated) |
| Head Office | Brisbane, QLD |
| Branch Office | Gold Coast, QLD |
| Remote Workers | 5 |
| Total Staff | 35 |
| MSP Provider | AlanTech Managed Services (ATMS) |

---

## IT Environment Summary

| Component | Details |
|-----------|---------|
| Microsoft 365 | Business Premium |
| Azure | Yes — VM, Backup, VPN |
| Windows Server | 2 x Windows Server 2022 |
| Domain | ad.brightbuild.com.au |
| NAS | Synology (file storage + backup) |
| VPN | Site-to-site (Brisbane ↔ Gold Coast) + Remote Access |
| Firewall | Business-grade (pfSense/similar) |
| Antivirus | Microsoft Defender (via Intune) |

---

## Departments

| Dept | Staff Count | Location |
|------|------------|----------|
| Management | 3 | Brisbane |
| Finance | 4 | Brisbane |
| HR | 2 | Brisbane |
| IT | 1 (us) | Brisbane |
| Operations | 10 | Brisbane |
| Site Engineers | 8 | On-site / Remote |
| Gold Coast Office | 7 | Gold Coast |

---

## Key Business Requirements

- Staff must access files from job sites (VPN / Teams / SharePoint)
- Email must always be available (Exchange Online)
- New employees must be onboarded within 1 business day
- Backups must run nightly and be tested monthly
- Passwords must meet compliance requirements (MFA enabled for all staff)

---

## Related Documents

- [Network Design](network-design.md)
- [Naming Convention](naming-convention.md)
- [IP Address Plan](ip-address-plan.md)
- [Active Directory Design](active-directory-design.md)
