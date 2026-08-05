# Adama Systems PLC — Infrastructure Architecture (Draft, Week 0)

## Purpose
This document describes the target IT infrastructure for Adama Systems PLC, a fictional engineering firm, as built during a self‑directed infrastructure engineering bootcamp. It covers the physical/logical topology, component roles, and design assumptions up to Week 4.

## Current State
As of Day 1, no infrastructure exists. We have a clean slate: one virtualisation host (the engineer’s laptop) and the software tools to build everything from scratch.

## Target State (End of Week 4)
By the end of Week 4, the following components will be operational and integrated:

- Internet connectivity (simulated via host NAT, later bridged)
- Firewall/Router device (will be implemented as a virtual firewall appliance or physical router in later stage; currently, conceptual)
- Switch (initially represented as a virtual network segment; later physical if hardware is available)
- Workstations: two or more Windows/Ubuntu client VMs for testing and user simulation
- Virtualisation Host: an Ubuntu Server running a Type 2 hypervisor (VirtualBox) with multiple VMs
- Servers: at minimum a file server, domain controller (Active Directory), and monitoring/logging server
- All infrastructure governed by the principle of no single point of failure where practical

## Diagram
Refer to `architecture-diagram.png` in this directory. The diagram shows the traffic flow: Internet → Firewall/Router → Switch → Servers and Workstations.

## Assumptions
- Single office location.
- Fewer than 50 users initially.
- All services will initially run on virtualised hardware within a single physical host (the engineer’s laptop), simulating a small‑office/data‑centre‑like environment.
- The bootcamp uses open‑source and free tools (VirtualBox, Ubuntu Server, pfSense or similar) to avoid vendor lock‑in and cost.

## Open Questions
- Will we simulate the firewall/router as a dedicated VM (e.g., pfSense), or will we use host‑based NAT and treat the concept separately? (Decision by Week 1.)
- How many workstations are needed to meaningfully test Active Directory and group policy? (Two minimum; perhaps three.)
- Should we segment internal traffic into separate VLANs for servers vs. workstations? (Yes, if time permits, as it teaches critical networking concepts.)
- What monitoring/alerting stack fits best with the available resources and learning goals? (Prometheus + Grafana vs. simpler tools — evaluate Week 2.)