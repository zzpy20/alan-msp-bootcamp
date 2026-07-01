# Naming Convention — BrightBuild Construction Pty Ltd

**Document:** Naming Convention v1.0
**Sprint:** Sprint 0 — Project Initiation
**Status:** Approved

---

## Convention Format

```
[SITE]-[ROLE]-[TYPE][NUMBER]
```

| Field | Options |
|-------|---------|
| SITE | BRIS = Brisbane HQ · GC = Gold Coast |
| ROLE | HO = Head Office · BR = Branch |
| TYPE | DC = Domain Controller · FS = File Server · APP = App Server · CLIENT = Workstation · PRINT = Print Server |
| NUMBER | 01, 02, 03 ... |

---

## Server Names

| Hostname | Role | Location |
|----------|------|----------|
| BRIS-HO-DC01 | Domain Controller (Primary) | Brisbane HQ |
| BRIS-HO-FS01 | File Services / Print Services | Brisbane HQ |
| GC-BR-DC01 | Domain Controller (Secondary) — future | Gold Coast |

---

## Workstation Names

| Hostname | User | Location |
|----------|------|----------|
| BRIS-HO-CLIENT01 | Finance Staff | Brisbane |
| BRIS-HO-CLIENT02 | Operations | Brisbane |
| BRIS-HO-CLIENT03 | Management | Brisbane |
| GC-BR-CLIENT01 | Gold Coast Staff | Gold Coast |

Workstations are named by location + role, not by user. If a user moves desks, the machine name stays the same.

---

## User Account Format

```
firstname.lastname@brightbuild.com.au
```

Examples:
- `john.smith@brightbuild.com.au`
- `sarah.jones@brightbuild.com.au`

Admin accounts use `-admin` suffix:
- `john.smith-admin@brightbuild.com.au`

---

## Group Names

```
GRP-[DEPT]-[PERMISSION]
```

Examples:
- `GRP-Finance-ReadOnly`
- `GRP-Finance-ReadWrite`
- `GRP-IT-Admins`
- `GRP-AllStaff`

---

## File Share Names

```
\\BRIS-HO-FS01\[DeptName]$
```

Examples:
- `\\BRIS-HO-FS01\Finance$`
- `\\BRIS-HO-FS01\HR$`
- `\\BRIS-HO-FS01\Shared$`
- `\\BRIS-HO-FS01\IT$`

---

## Why This Matters

At an MSP, you manage 10–30 clients simultaneously. If every server is named "Server01", you will make mistakes. Enterprise naming tells you instantly: what it is, where it is, and what it does — without logging in.
