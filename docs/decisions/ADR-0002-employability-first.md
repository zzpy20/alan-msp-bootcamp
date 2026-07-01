# ADR-0002 — Optimise for Employability, Not Knowledge

**Date:** 2026-07-02
**Status:** Accepted
**Sprint:** Sprint 0 — Project Initiation

---

## Decision

> **We optimise for employability, not knowledge.**

The goal of this bootcamp is not to accumulate the most IT knowledge. It is to reach "enterprise will hire this person" as fast as possible.

---

## The Filter

Before adding any topic, lab, or skill to the bootcamp, ask:

> *"Does a Junior MSP Engineer in Brisbane encounter this in their first 6 months?"*

| Answer | Action |
|--------|--------|
| Yes, commonly | Learn it. Practice it until confident. |
| Sometimes, but not critical | Note it, defer to later |
| Rarely / advanced only | Skip entirely |

---

## What This Means in Practice

**We will skip things that are:**
- Academically interesting but not in Junior MSP job ads
- Advanced topics that come after 2+ years of experience
- Certifications that don't reflect real-world MSP work

**We will drill things that are:**
- Basic and boring but appear in every MSP environment
- Commonly asked in Brisbane MSP interviews
- Things a new hire is expected to handle on day one

---

## Examples

| Topic | Decision | Reason |
|-------|----------|--------|
| Active Directory basics | Learn deeply | Every MSP, every day |
| DNS / DHCP | Learn deeply | Every MSP, every day |
| Microsoft 365 admin | Learn deeply | 88% of Brisbane MSP job ads |
| Kubernetes | Skip (for now) | Not in Junior MSP role |
| Terraform | Skip (for now) | Not in Junior MSP role |
| PowerShell basics | Learn | Appears in 36% of MSP job ads |
| Group Policy | Learn deeply | Every MSP, every day |

---

## Relationship to ADR-0001

ADR-0001 says: *Enterprise Standard → MSP Reality → SMB Budget.*
ADR-0002 says: *Employability over knowledge.*

They work together. ADR-0001 filters design decisions. ADR-0002 filters what we spend time learning.
