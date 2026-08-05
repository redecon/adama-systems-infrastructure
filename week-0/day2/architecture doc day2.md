# Adama Systems PLC — Infrastructure Architecture (Draft, Week 0)

## Purpose
This document describes the target IT infrastructure for Adama Systems PLC, a fictional engineering firm, as built during a self‑directed infrastructure engineering bootcamp. It covers the physical/logical topology, component roles, and design decisions up to Week 4.

## Current State
As of Day 2, we have a single Ubuntu Server VM running on VirtualBox (Type 2 hypervisor), staged with Bridged networking and a clean‑install snapshot. The architecture is still conceptual; physical hardware has not been purchased. The Day 2 procurement list and this document define the target state.

## Target State (End of Week 4)
Same as Day 1, plus the hardware and OS specifics now defined.

## Server & Storage Plan (added Day 2)

### Server Roles
- **Domain Controller (replica):** Windows Server 2022 VM, provides local authentication if WAN link to head office fails.
- **File & Print Server:** Windows Server 2022 VM, SMB shares with AD permissions.
- **Monitoring Server:** Ubuntu Server LTS VM, runs Prometheus, Grafana, and syslog.
- **Internal Wiki Server:** Ubuntu Server LTS VM, lightweight documentation platform.

All VMs will run on a single physical host with a Type 1 hypervisor (ESXi or Proxmox) in the branch office.

### Storage / RAID Approach
- Four 2 TB enterprise SATA disks in **RAID 10** (striped mirrors).
- Justification: RAID 10 offers fast read/write performance and the ability to survive a disk failure with a quick rebuild time. The 4 TB usable capacity is sufficient for the branch office’s file shares and VM storage. We accept the 50% storage efficiency to avoid the long rebuild and second‑disk‑failure risk of RAID 5.

### OS per Server Role
- Windows Server 2022 for domain controller and file server: ensures seamless Active Directory integration and matches existing IT skills.
- Ubuntu Server LTS for monitoring and wiki: eliminates per‑user licensing costs and runs open‑source tools natively.

## Network Configuration Notes (added Day 2)
- All lab VMs have been reconfigured from NAT to **Bridged** mode in VirtualBox.
- This gives each VM its own IP on the physical LAN, enabling direct communication between VMs (necessary for domain join, file sharing, and monitoring) starting Week 1.
- The host machine is the bridge to the internet; no additional virtual router is used.

## Diagram
Refer to `architecture-diagram.png`. The topology is unchanged: Internet → Firewall/Router → Switch → VMs and workstations.

## Assumptions
- Single branch office with fewer than 30 users.
- Stable WAN link to main office for directory replication.
- Physical server will be ordered and installed by Week 4 (in simulation; in bootcamp, it remains virtualised on the engineer’s laptop).

## Open Questions
- Which Type 1 hypervisor (ESXi free vs. Proxmox) will be simulated? (Decision by Week 2.)
- Do we need a local DHCP/DNS server, or will the firewall/router provide these? (To be resolved in network design.)
- Backup strategy details: will we use Veeam Community Edition or a simpler script‑based approach? (Week 3.)