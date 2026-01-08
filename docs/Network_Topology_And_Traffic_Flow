## Network Topology & Traffic Flow

### Overview
This server is deployed on a Debian-based Linux system hosting an Evennia
multiplayer game service. The project demonstrates core networking concepts
including client/server architecture, TCP services, firewall policy enforcement,
and NAT-based WAN exposure.

The topology separates **management access** from **service access** and
documents how traffic flows from external clients to the application layer.

---

### Network Topology Diagram

```text
                ┌──────────────────────┐
                │   Remote Client      │
                │ (Telnet / SSH / CLI) │
                └──────────┬───────────┘
                           │ TCP 4000
                    (Internet / WAN)
                           │
                ┌──────────▼───────────┐
                │   Home Router / NAT   │
                │  Port Forwarding     │
                │  TCP 4000 → Server   │
                └──────────┬───────────┘
                           │
                    (LAN 192.168.1.0/24)
                           │
                ┌──────────▼───────────┐
                │ Debian Evennia Server│
                │----------------------│
                │ - nftables / iptables│
                │ - systemd            │
                │ - SSH (22, LAN only) │
                │ - Evennia (4000)     │
                └──────────┬───────────┘
                           │
                ┌──────────▼───────────┐
                │ Evennia Game Process │
                │ (Python / Twisted)  │
                └──────────────────────┘
