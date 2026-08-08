# Packet Capture Analysis Report — Day 3

## Capture Details
- **Date/time:** [2026-08-07, 10:00–10:03 UTC]
- **Duration:** 3 minutes
- **Interface captured:** [Wi‑Fi (en0)]


## Protocols Identified
| Protocol | Purpose in this capture | Frame # example |
|---|---|---|
| ARP | Resolved local IP addresses to MAC addresses; e.g., my laptop asked for the MAC of the default gateway. | [123, 124] |
| DNS | Translated domain names (e.g., example.com) to IP addresses so applications could establish connections. | [200, 201] |
| TCP | Provided reliable, connection‑oriented data transfer; a three‑way handshake (SYN, SYN‑ACK, ACK) preceded HTTP. | [456] |
| HTTP | Carried a plain‑text web request and response (to neverssl.com). | [500] |

## Layer 2 vs Layer 3 Observation
In frame [200] (a DNS query to 8.8.8.8):
- **Ethernet II source MAC:** [aa:bb:cc:dd:ee:ff] (my laptop’s NIC)
- **Ethernet II destination MAC:** [00:11:22:33:44:55] (my home router’s MAC)
- **IPv4 source IP:** [192.168.1.100] (my laptop)
- **IPv4 destination IP:** [8.8.8.8] (Google’s DNS server)

The destination MAC address belongs to my local router, **not** to the remote server (8.8.8.8). This is because MAC addresses only carry the frame as far as the next Layer 3 hop; the router will de‑capsulate the packet, consult its routing table, and then re‑encapsulate it into a new frame with a different MAC for the next link. The IP addresses, however, remain the same end‑to‑end. This is exactly why the OSI model separates Layer 2 (local delivery) from Layer 3 (global addressing).

## Key Takeaway
Reading about the OSI model gave me a static, layered diagram. Capturing live traffic and stepping through real ARP, DNS, and TCP handshakes made it dynamic. I could *see* the broadcast ARP request go out, the DNS query resolve a name, and the SYN flag set in the first TCP packet. The most striking moment was comparing the destination MAC (my router) with the destination IP (a remote server) in the same frame — that single observation proved that Layer 2 and Layer 3 addresses serve completely different purposes, and that routers must strip and rebuild frames at every hop. This exercise turned theoretical knowledge into a diagnostic skill I can use to troubleshoot real connectivity problems.