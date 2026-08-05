## Memorandum

To: Senior Management, Adama Systems PLC
From: Rediet Bekele, Infrastructure Engineer
Date: Day 1 – Week 0
Subject: IT Infrastructure Overview for Adama Systems PLC

## Purpose
This memo explains, in non‑technical terms, the core IT infrastructure Adama Systems needs to operate reliably, securely, and cost‑effectively. It also outlines the target setup we will have in place by the end of Week 4.

## Why We Need This Infrastructure
Every modern business depends on three things: communication (email, internet), data storage (files, customer records), and secure operations. Without a properly designed underlying system, these daily activities are slow, vulnerable to attack, and prone to sudden failure. The goal of the infrastructure I’m designing is to make sure our team can work without ever worrying about whether the computers and network are functioning—just like a reliable electricity supply.

## What We Will Build (in Plain Terms)
1. Internet Connection
A commercial internet link from a local provider. This is our gateway to the outside world—it lets us send email, browse the web, and, later, host services for remote workers.

2. Firewall / Router
A single device that does two jobs:

Firewall – acts as a security guard that checks everything coming from the internet. It stops hackers, viruses, and unauthorised access before they can touch our internal systems.

Router – acts as a traffic director, making sure data from the internet goes to the right internal computer, and that internal requests get out to the web quickly. Without it, our private office network couldn’t safely connect to the internet.

3. Switch
Think of the switch as an intelligent power strip for data. It connects all our office computers and servers together, allowing them to share files and printers directly without needing to go out to the internet. It’s fast, silent, and handles all internal conversations.

4. Virtualisation Host (Server)
A single, powerful physical computer that runs special software (called a hypervisor) to create multiple “virtual computers” inside itself. Each virtual computer behaves like a real, independent machine. Why we do this:

- Cost savings – we can run many business applications (file sharing, authentication, website testing) on one piece of hardware instead of buying a separate machine for each.

- Flexibility – we can add or remove virtual computers in minutes without ordering new hardware.

- Reliability – if a virtual machine crashes, the host keeps others running, and we can restore a clean backup (called a snapshot) in seconds.

5. Workstations
Standard desktop or laptop computers for our staff. They will plug into the switch to access files, email, and business applications. We’ll start with a small number, easily expandable.

6. Redundancy Philosophy (the “don’t put all your eggs in one basket” approach)
In the physical world, we’ll later ensure the server has two separate power feeds (where practical) and backup battery support. On the network side, we’ll configure things so that a single cable coming loose doesn’t stop the entire office. In short: we assume something will eventually fail, and we design so that no single failure causes a work stoppage. This is exactly the same thinking that keeps industrial plants running safely.

## What We Will Have by Week 4
By the end of this bootcamp’s first four weeks, our fictional company will have:

- A functioning office network with internet access, firewall/router, and switch.

- A virtualisation host running critical services like file storage and user authentication.

- A secure environment that can be expanded to cloud services or more users without re‑engineering the whole system.