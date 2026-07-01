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
│   ├── Computers
│   │   ├── Brisbane
│   │   └── GoldCoast
│   ├── Users
│   │   ├── Brisbane
│   │   └── GoldCoast
│   ├── Groups
│   ├── Servers
│   └── ServiceAccounts
└── Domain Controllers (default)
```

**Why the underscore prefix on `_BRIGHTBUILD`?**
It sorts to the top of the OU list. When you manage 20 clients, you don't want to scroll. Enterprise habit.

**Why a custom OU instead of using defaults?**
Default containers (CN=Users, CN=Computers) cannot have Group Policy applied to them. All real deployments use custom OUs.

---

## User Accounts

### Standard User Template

| Field | Value |
|-------|-------|
| UPN Format | firstname.lastname@brightbuild.com.au |
| Password Policy | Min 12 chars, complexity on, 90-day expiry |
| MFA | Required (enforced via Entra ID) |
| Home Drive | \\BRIS-HO-FS01\Users\%username% (H:) |
| Logon Script | GPO-applied (map drives, set printers) |

### Sample Users to Create in Lab

| Name | Username | Dept | OU |
|------|----------|------|----|
| John Smith | john.smith | Finance | Users/Brisbane |
| Sarah Jones | sarah.jones | HR | Users/Brisbane |
| Mike Chen | mike.chen | IT | Users/Brisbane |
| Lisa Brown | lisa.brown | Management | Users/Brisbane |
| Tom Wilson | tom.wilson | Operations | Users/GoldCoast |

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
| GPO-DriveMapping | Users/Brisbane | Map H: and shared drives |
| GPO-DesktopWallpaper | All Computers | Corporate wallpaper |
| GPO-DisableUSB | All Computers | Block USB storage (security) |
| GPO-WindowsUpdate | All Computers | Force updates via WSUS |
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
