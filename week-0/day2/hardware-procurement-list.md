# Hardware Procurement List — Adama Systems PLC (Branch Office)

## 1. Server Hardware

| Item | Specification | Justification |
|------|---------------|---------------|
| **Form factor** | 2U rack‑mount server | Standard enterprise size; fits a small wall‑mount rack in a comms room. 2U allows more drive bays and larger, quieter fans than 1U — better for a branch office that may not have a dedicated data centre. |
| **CPU** | 1 × Intel Xeon E‑2300 series, 6‑core | Enough to run multiple virtual machines (domain controller, file server, monitoring) without over‑subscribing the host. A single socket keeps licensing costs predictable (Windows Server is licensed per core). |
| **RAM** | 32 GB DDR4 ECC | Error‑correcting memory is non‑negotiable for any server holding business data. 32 GB gives headroom to run 3–4 VMs comfortably (DC: 4 GB, file server: 4 GB, monitoring: 2 GB, plus hypervisor overhead). |
| **Storage** | 4 × 2 TB enterprise SATA HDD (hot‑swap) | Four disks allow RAID 10 (see below). Hot‑swap means a failed disk can be replaced without powering off the server — crucial for a remote office with no on‑site IT staff. |
| **RAID controller** | Hardware RAID controller with battery‑backed cache | Offloads RAID calculations from the CPU and protects in‑flight writes during a power loss. |
| **Power supplies** | Dual, hot‑plug redundant (2 × 550W) | One power supply can fail without taking the server down. Each supply connects to a separate power feed (or at least a separate circuit) — the same philosophy as dual feeds to a control panel. |
| **Network** | 4 × 1 GbE ports (on‑board + additional NIC) | At least two ports for teaming (link aggregation) to the office switch; extra ports for management network or future iSCSI storage. |
| **Mounting** | Tool‑less sliding rails + cable management arm | Makes servicing easy; the server slides out without disconnecting cables. |
| **Estimated unit cost** | $3,500–$4,500 (typical for this class) | Reasonable for a branch office; total cost of ownership is far lower than buying multiple smaller servers. |

## 2. Storage Approach and RAID Choice

**RAID level: RAID 10 (a stripe of mirrored pairs)**

**Why:**
- **Performance:** Both reads and writes are fast — writes are a simple mirror (no parity calculation), reads can be split across mirrors. Ideal for a mixed workload (file sharing, Active Directory database, logging).
- **Redundancy:** Can survive any single disk failure, and possibly two (if the second failure is in a different mirror pair). Rebuild time is fast: only copying data from the surviving mirror, not recalculating parity.
- **Capacity:** With four 2 TB disks, usable space is 4 TB (50% efficiency). This is acceptable for a branch office where 4 TB of actual storage is enough for file shares, user profiles, and operating system VHDs.
- **Trade‑off acknowledged:** RAID 10 is more expensive in disk count per usable terabyte than RAID 5. However, for a branch office with a single server, the risk of a second disk failing during a long RAID 5 rebuild (which could destroy all data) is unacceptable. **We prioritise uptime and rebuild speed over raw capacity efficiency.** This is the same thinking as choosing dual‑redundant sensors over a single sensor with a spare on a shelf.

**Note:** RAID is not a backup. We will back up the server to a NAS in the main office (or to cloud storage) weekly, with daily incremental backups.

## 3. Operating System Choice per Server Role

This server will run a **Type 1 hypervisor** (VMware ESXi free edition or Proxmox VE) to host multiple virtual machines. Each VM’s OS is chosen based on its function.

| Role | OS | Business Justification |
|------|----|------------------------|
| **Domain Controller (replica)** | Windows Server 2022 | The main office already uses Active Directory. A Windows Server replica DC integrates natively, replicates authentication data, and lets branch users log in even if the WAN link to head office fails. The IT team is already Windows‑trained. |
| **File & Print Server** | Windows Server 2022 | Windows file sharing (SMB) provides seamless access for Windows‑based workstations, integrates with AD permissions, and supports features like Volume Shadow Copy for self‑service file recovery. |
| **Monitoring & Logging Server** | Ubuntu Server LTS | Zero licensing cost for the OS; runs industry‑standard open‑source monitoring tools (Prometheus, Grafana, ELK stack) that are Linux‑native. This server only needs to be accessible by the IT team, so the lack of a GUI is not a problem. |
| **Internal Wiki / Documentation** | Ubuntu Server LTS | Lightweight, runs on minimal resources, and the wiki software (e.g., Wiki.js, BookStack) is open‑source and runs best on Linux. Again, no per‑user licence fees. |

**Why we use a mix:** Windows pays for itself through tight AD integration and familiar support. Linux reduces cost for commodity web services and tooling. This is a normal, rational hybrid environment — not a religious choice.