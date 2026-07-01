# Active Directory Design — BrightBuild Construction Pty Ltd

**Document:** Active Directory Design v1.0
**Sprint:** Sprint 0 — Project Initiation
**Status:** Approved

---

## Domain Information

| Field | Value |
|-------|-------|
| Domain Name | ad.brightbuild.com.au |
| Why not .local? | `.local` conflicts with mDNS, breaks certificate issuance, complicates Entra ID sync. Microsoft stopped recommending it years ago. |
| Forest / Domain Level | Windows Server 2022 |
| Domain Controller | BRIS-HO-DC01 (10.10.10.10) |
| Secondary DC | GC-BR-DC01 (future — Sprint 3) |
| Entra ID Sync | Yes — via Microsoft Entra Connect |
| Public Domain | brightbuild.com.au (Microsoft 365) |

---

## OU Structure

```
ad.brightbuild.com.au
├── _BRIGHTBUILD
│   ├── Users
│   │   ├── Finance
│   │   ├── HR
│   │   ├── Management
│   │   ├── IT
│   │   └── Operations
│   ├── Computers
│   ├── Servers
│   ├── Groups
│   └── ServiceAccounts
└── Domain Controllers (default)
```

**Why the underscore prefix on `_BRIGHTBUILD`?**
It sorts to the top of the OU list. When you manage 20 clients, you don't want to scroll. Enterprise habit.

**Why a custom OU instead of using defaults?**
Default containers (CN=Users, CN=Computers) cannot have Group Policy applied to them. All real deployments use custom OUs.

**Why department-based OUs, not location-based?**
Group Policy is almost always applied by department logic — Finance needs Finance drive mappings, Finance printers, Finance software — regardless of which office they sit in. A Gold Coast Finance user is still Finance. Location is an attribute on the user object (City, Office fields), not a structural container. If we used location-based OUs, we'd need duplicate GPOs for every department in every city. Department OUs scale cleanly as the company grows.

---

## User Accounts

### Standard User Template

| Field | Value |
|-------|-------|
| UPN Format | firstname.lastname@brightbuild.com.au |
| Password Policy | Min 12 chars, complexity on, **no expiry** |
| MFA | Required for all users (Entra ID) |
| Conditional Access | Block legacy auth, enforce MFA, require compliant device |
| Risk Detection | Entra ID Protection — auto-block risky sign-ins |
| Home Drive | \\BRIS-HO-FS01\Users\%username% (H:) |
| Logon Script | GPO-applied (map drives, set printers) |

**Why no password expiry?**
Microsoft removed periodic password expiry from their security baseline in 2019. Forced rotation produces weaker passwords — users increment numbers (`Password1!` → `Password2!`) rather than choosing stronger ones. Modern identity security relies on MFA + Conditional Access + breach detection, not rotation. If a password is compromised, Entra ID Protection detects the risky sign-in and blocks it — expiry wouldn't have helped anyway.

**Why not WSUS?**
WSUS requires a dedicated server, disk storage for update files, and ongoing maintenance. For a 35-user company this is unnecessary overhead. Windows Update for Business (WUfB) delivers the same control (deferral rings, targeting) via GPO with no server. Phase 2 migrates this to Intune, which is already included in their M365 Business Premium licence.

**Modern Identity stack (Phase 2 — Sprint 3+):**
- Entra ID MFA (already enforced)
- Conditional Access policies (block legacy auth, require MFA from outside office)
- Entra ID Protection (risk-based sign-in blocking)
- Password Protection (ban common/weak passwords via Entra)

### Sample Users to Create in Lab

| Name | Username | Dept | OU |
|------|----------|------|----|
| John Smith | john.smith | Finance | Users/Finance |
| Sarah Jones | sarah.jones | HR | Users/HR |
| Mike Chen | mike.chen | IT | Users/IT |
| Lisa Brown | lisa.brown | Management | Users/Management |
| Tom Wilson | tom.wilson | Operations | Users/Operations |

---

## Security Groups

| Group Name | Type | Purpose |
|------------|------|---------|
| GRP-AllStaff | Security | All users — base access |
| GRP-Finance-RW | Security | Finance shared drive read/write |
| GRP-HR-RW | Security | HR shared drive read/write |
| GRP-IT-Admins | Security | IT admin access |
| GRP-Management-RW | Security | Management files |
| GRP-Remote-VPN | Security | Users allowed VPN access |

---

## Group Policy Objects (GPOs)

| GPO Name | Applied To | Purpose |
|----------|-----------|---------|
| GPO-PasswordPolicy | Domain | Password complexity + expiry |
| GPO-DriveMapping-Finance | Users/Finance | Map H:, F: (Finance share) |
| GPO-DriveMapping-HR | Users/HR | Map H:, R: (HR share) |
| GPO-DriveMapping-AllStaff | Users | Map H:, S: (Shared) |
| GPO-DesktopWallpaper | All Computers | Corporate wallpaper |
| GPO-DisableUSB | All Computers | Block USB storage (security) |
| GPO-WindowsUpdate | All Computers | Windows Update for Business — defer feature updates 30 days, quality updates 7 days |
| GPO-LocalAdminRestrict | All Computers | Remove local admin from standard users |
| GPO-ScreenLock | All Computers | Lock after 10 min idle |

---

## Drive Mapping Plan

| Drive Letter | Path | Who Gets It |
|-------------|------|------------|
| H: | \\BRIS-HO-FS01\Users\%username% | All users (home drive) |
| S: | \\BRIS-HO-FS01\Shared$ | GRP-AllStaff |
| F: | \\BRIS-HO-FS01\Finance$ | GRP-Finance-RW |
| R: | \\BRIS-HO-FS01\HR$ | GRP-HR-RW |

---

## Sprint 1 Lab Targets

Build this and confirm with screenshots:

- [ ] Install AD DS on BRIS-HO-DC01
- [ ] Promote to Domain Controller (domain: ad.brightbuild.com.au)
- [ ] Create OU structure as designed above
- [ ] Create 5 sample users
- [ ] Create security groups and add users
- [ ] Join CLIENT01 (Windows 11) to domain
- [ ] Login with domain user account
- [ ] Confirm AD structure matches this document

---

## Related Documents

- [Enterprise Overview](enterprise-overview.md)
- [Naming Convention](naming-convention.md)
- [IP Address Plan](ip-address-plan.md)
- [Network Design](network-design.md)
