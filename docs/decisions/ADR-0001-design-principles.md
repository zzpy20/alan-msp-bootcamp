# ADR-0001 — Design Principles

**Date:** 2026-07-02
**Status:** Accepted
**Sprint:** Sprint 0 — Project Initiation

---

## Decision

All architecture and design decisions in this bootcamp must satisfy three criteria, in order:

```
Enterprise Standard
       ↓
  MSP Reality
       ↓
  SMB Budget
```

---

## Context

This bootcamp targets Junior MSP Engineer / Systems Administrator roles in Brisbane, Australia, serving companies of 30–100 staff.

Microsoft publishes best practices designed for large enterprises with dedicated IT teams, unlimited Azure spend, and full licensing. Real Australian SMBs operate differently:

- A 35-person construction company will not run Entra Connect + Hybrid AD + full Azure stack on day one
- Budget is a real constraint — every design decision has a cost implication
- MSP engineers work within client budgets, not Microsoft's product roadmap
- "Enterprise" in this context means professional standards and naming — not enterprise-grade spending

---

## The Three Criteria

### 1. Enterprise Standard
The design must follow professional standards:
- Correct naming conventions
- Proper security posture
- Documented and repeatable
- Scalable if the business grows

### 2. MSP Reality
The design must reflect what MSPs actually deploy:
- What do Brisbane MSP job ads actually list?
- What does a Level 1/2 engineer encounter on day one?
- Not theoretical — what is running in production at real clients?

### 3. SMB Budget
The design must be affordable for a 30–100 person Australian company:
- Prefer included licences over additional spend (M365 Business Premium already includes Intune, Defender, Entra ID P1)
- Avoid solutions that require dedicated headcount to maintain (e.g. WSUS, on-prem Exchange)
- Cloud-first where it reduces operational overhead, on-prem where it reduces cost

---

## Consequences

Every time we make a design choice, we ask:

> *"Would a real Brisbane MSP deploy this for a 35-person client?"*

If the answer is No — we redesign, simplify, or defer it.

This also means we will sometimes deliberately NOT follow Microsoft's recommended approach if it is over-engineered for the context. We document why.

---

## Examples Applied

| Topic | Microsoft Luxury | Our Decision | Reason |
|-------|-----------------|--------------|--------|
| Domain | `.local` (legacy) | `ad.brightbuild.com.au` | Hybrid-ready, cert-friendly |
| Updates | WSUS | Windows Update for Business | No server overhead for 35 users |
| Identity | Full Entra Hybrid | Entra ID cloud-only (Phase 1) | Most SMBs don't run Hybrid |
| Password | 90-day rotation | No expiry + MFA | Modern Identity, Microsoft's own guidance |

---

## Review

This decision applies to the entire bootcamp. If a future design conflicts with these principles, the design must be revisited — not the principles.
