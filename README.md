# Alan MSP Bootcamp

**Objective:** Become employable as an MSP Engineer / Systems Administrator / Infrastructure Support Engineer in Brisbane, Australia.

This is not a course. This is a job simulation.

Every task, ticket, and document in this repo was completed as if working for a real MSP client — **BrightBuild Construction Pty Ltd** — a 35-person construction company with offices in Brisbane and Gold Coast.

---

## The Company We Support

**Client:** BrightBuild Construction Pty Ltd
**Industry:** Construction
**Size:** 35 employees
**Locations:** Brisbane (HQ) + Gold Coast (Branch) + 5 Remote Workers
**Stack:** Microsoft 365 Business Premium · Azure · Windows Server · Synology NAS · VPN

---

## Bootcamp Structure

Organized as Agile Sprints, not weekly lessons.

| Phase | Sprints | Focus | Target |
|-------|---------|-------|--------|
| Phase 1 | Sprint 0–2 | Enterprise Windows Infrastructure | Junior MSP |
| Phase 2 | Sprint 3–5 | Cloud — Azure / M365 / Hybrid | MSP L2 |
| Phase 3 | Sprint 6–8 | Tickets / Docs / Interview / Job Hunt | Employed |

**Sprint 0:** Project Initiation — Architecture, naming conventions, IP plan, AD design

---

## Repository Structure

```
alan-msp-bootcamp/
├── docs/
│   └── architecture/       # Enterprise design docs (Sprint 0 deliverables)
├── labs/
│   ├── sprint-01/          # Lab notes, configs, VM setup
│   └── sprint-02/
├── scripts/                # PowerShell, Bash automation
├── tickets/                # Simulated MSP helpdesk tickets
├── portfolio/              # Final showcase projects
├── screenshots/            # Lab evidence
├── interview-notes/        # Interview prep
└── assets/                 # Diagrams, reference files
```

---

## Current Progress

See [PROGRESS.md](PROGRESS.md) for full skill tracker.

```
MSP Job Readiness     ████░░░░░░  35%   Sprint 0 complete — Sprint 1 starting
```

---

## Design Principles

> **[ADR-0001](docs/decisions/ADR-0001-design-principles.md) — Every design decision must satisfy:**
> ```
> Enterprise Standard → MSP Reality → SMB Budget
> ```
> Not Microsoft's most expensive solution. What a real Brisbane MSP deploys for a 30–100 person client.

---

## Bootcamp Rules

1. **Everything has a reason** — we only learn what Brisbane MSP jobs actually require
2. **Always Enterprise** — enterprise naming, enterprise mindset (BRIS-HO-DC01, not "myserver")
3. **Documentation First** — every lab gets documented before moving on
4. **Git Everything** — PowerShell, configs, markdown — all committed
5. **Production Mindset** — before every action: *"Would I do this on a client's system?"*

---

## Current Sprint

**Sprint 0 — Project Initiation**
> As an MSP engineer, I want to design a standard enterprise network so that future deployments are consistent.

Deliverables: Enterprise overview · Network design · Naming convention · IP address plan · AD design

---

*Built with Claude Code. Managed like a real project.*
