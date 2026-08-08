# Adama Systems Infrastructure

A documented, step‑by‑step build of a fictional engineering firm’s IT infrastructure, created as part of a self‑directed **Infrastructure Engineering Bootcamp**.

## What This Project Is

This repository is my **learning portfolio** — a hands‑on journey from zero infrastructure to a fully functioning enterprise IT environment. Over several weeks, I design, build, and document:

- Physical and virtual server hardware decisions
- Network topologies (firewall, router, switch, VLANs)
- Virtualisation (Type 1 and Type 2 hypervisors, VM provisioning)
- Storage architecture (RAID planning, file servers)
- Windows Server services (Active Directory, DNS, DHCP, Group Policy)
- Linux server administration (Ubuntu Server, monitoring, scripting)
- Infrastructure as Code and automation basics
- Monitoring, logging, and troubleshooting

Everything is built around **Adama Systems PLC** — a fictional company that gives context to every design decision. The infrastructure is not just configured; it’s justified in business terms, exactly as I would in a real engineering role.

## Why This Repo Exists

Most bootcamps teach you to pass a test. This one — which I designed for myself — teaches me to **think, build, and explain** like an infrastructure engineer. Every day includes:

- Deep conceptual understanding (not just how, but *why*)
- Hands‑on labs (real VMs, real networks, real break‑fix)
- Mini‑projects (architecture diagrams, procurement lists, business memos)
- Portfolio‑ready documentation (the very files in this repo)
- Interview‑style questions and daily skill gates

My background in **control systems engineering** gives me an edge: I already think in terms of redundancy, feedback loops, failure modes, and distributed systems. This bootcamp translates that intuition into the IT domain, preparing me for roles in system administration, cloud engineering, or site reliability engineering.

I also hold the **AWS Cloud Practitioner** certification, which gives me the cloud side of the shared responsibility model. Here, I’m building the other side — the on‑premises and virtualised infrastructure that runs beneath the cloud.

## Repository Structure
adama-systems-infrastructure/
├── README.md ← You are here
├── week-0/ ← Foundations & mental models
│ ├── day-1/ ← Hypervisor install, topology, memo
│ ├── day-2/ ← Server form factors, RAID, OS decisions, VM networking
│ └── ... ← Days 3–7 (as the bootcamp progresses)
├── week-1/ ← Linux command line, networking fundamentals
├── week-2/ ← Windows Server, Active Directory, Group Policy
├── week-3/ ← Infrastructure as Code, monitoring, backups
├── week-4/ ← Integration, automation, capstone project
└── assets/ ← Shared diagrams, reference images

Each day’s folder typically contains:

- **`architecture-diagram.png`** – visual topology or design
- **`*.md` documents** – business memos, procurement lists, decision logs
- **`screenshots/`** – verification of lab work (VM setup, snapshots, configurations)

## Key Artifacts (So Far)

| Day | Artifact | Description |
|-----|----------|-------------|
| Day 1 | `infrastructure-overview-memo.md` | Plain‑language explanation of IT infrastructure for non‑technical managers |
| Day 1 | `architecture-diagram.png` | First enterprise network topology (Internet → Firewall → Switch → Devices) |
| Day 2 | `hardware-procurement-list.md` | Branch‑office server build with RAID, form factor, and OS justifications |
| Day 2 | `architecture-document.md` | Living architecture document, updated daily |

## Core Philosophy

- **No step without a reason.** Every configuration choice is tied to a business requirement or engineering trade‑off.
- **Documentation is a first‑class deliverable.** A working system without clear explanations is incomplete.
- **Assume failure, design for resilience.** Redundant power, RAID, snapshots, backup strategies — the same mindset as industrial control systems.
- **Show your work.** Commits are descriptive; screenshots are evidence; reflections capture learning.

## About Me

I’m an infrastructure engineer in training, bridging a background in **control and automation systems** with modern IT operations. I learn best by building, breaking, and documenting — and this repository is that process made public.

If you’re a hiring manager or fellow engineer looking at this, I hope you see not just a collection of labs, but a mindset: systematic, business‑aware, and relentlessly curious about how things work under the hood.

---

*This bootcamp is self‑directed and ongoing. The repository will evolve daily as new concepts and configurations are added.*