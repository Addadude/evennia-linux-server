# Linux-Based Multiplayer Server (Evennia)

## Overview

This repository documents the deployment, administration, and troubleshooting of a **Linux-based multiplayer game server** built using the **Evennia** framework. The project is designed as a hands-on learning environment to develop practical skills in:

* Linux system administration
* Networking fundamentals
* Firewall configuration
* Client–server architecture
* Structured troubleshooting using the OSI model

Rather than focusing only on configuration files, this repository emphasizes **how problems are diagnosed and solved in real systems**.

---

## Project Goals

* Deploy and operate an Evennia server on Linux
* Expose the server to local and wide-area networks
* Secure the server using host-based firewalls
* Understand and document client-to-server connection behavior
* Troubleshoot connectivity issues using the OSI model

---

## Documentation

The following documents capture the technical reasoning and troubleshooting methods used in this project:

* **[OSI Model – Practical Cheat Sheet](OSI_Model_Cheat_Sheet.md)**
  A one-page, hands-on reference mapping OSI layers to real Linux networking commands, including a real-world Evennia connection failure walkthrough.

---

## Key Concepts Demonstrated

* Client–host communication and TCP connections
* Port management and service binding
* Firewall rule evaluation and traffic filtering
* Network isolation using layered troubleshooting
* Translating theoretical models (OSI) into real-world diagnostics

---

## Tools & Technologies

* Linux (Debian-based)
* Evennia (Python-based MUD/MU* framework)
* systemd
* iproute2 (`ip`, `ss`)
* ufw / iptables
* SSH, Telnet

---

## Why This Repository Exists

This repository serves as a **learning log and technical portfolio**, demonstrating not only *what* was built, but *how* issues were identified and resolved. The documentation is intended to reflect real operational thinking used in system and network administration roles.

---

## Firewall & OSI Layer Mapping

This section explains how **firewalls interact with specific OSI layers** and how firewall misconfigurations commonly cause connection failures.

---

### Where Firewalls Operate in the OSI Model

| OSI Layer             | Firewall Role                                    | Practical Meaning                                  |
| --------------------- | ------------------------------------------------ | -------------------------------------------------- |
| Layer 7 – Application | Application-aware filtering (advanced firewalls) | Inspect protocols like HTTP, SSH, or game traffic  |
| Layer 4 – Transport   | **Primary firewall layer**                       | Allow or block TCP/UDP ports                       |
| Layer 3 – Network     | IP-based filtering                               | Allow or deny traffic from specific IPs or subnets |

Most host-based firewalls (such as **ufw**, **iptables**, or **nftables**) operate mainly at **Layers 3 and 4**.

---

### Firewall Example — Evennia Server

**Goal:** Allow external players to connect to an Evennia server on TCP port 4000 while blocking unnecessary access.

#### Layer 4 — Transport (Port Control)

```bash
sudo ufw allow 4000/tcp
```

* Allows TCP connections to the Evennia service
* If this rule is missing, clients will see timeouts or connection refusals

---

#### Layer 3 — Network (IP Filtering)

```bash
sudo ufw allow from 192.168.1.0/24 to any port 22 proto tcp
```

* Restricts SSH access to the local network
* Reduces attack surface

---

### Common Firewall Failure Patterns (Mapped to OSI)

| Symptom                        | OSI Layer                    | Likely Cause                                  |
| ------------------------------ | ---------------------------- | --------------------------------------------- |
| Connection times out           | Layer 4                      | Port blocked by firewall                      |
| Connection refused             | Layer 4                      | Service not listening or firewall reject rule |
| Can ping but can’t connect     | Layer 3 OK / Layer 4 failing | Port not allowed                              |
| Works locally but not remotely | Layer 3 / NAT                | Router port forwarding missing                |

---

### Troubleshooting Firewall Issues Using OSI

1. **Layer 3:** Can the client reach the host IP?

   ```bash
   ping server_ip
   ```

2. **Layer 4:** Is the port reachable?

   ```bash
   nc -zv server_ip 4000
   ```

3. **Layer 7:** Is the application responding?

   ```bash
   telnet server_ip 4000
   ```

---

### Key Takeaway

> Firewalls do not "break the network" — they deliberately block traffic at specific OSI layers. Understanding *which* layer is affected makes firewall issues predictable and easy to diagnose.

---

## Future Additions

* Network diagrams (LAN / WAN)
* Automation scripts for server setup
* Expanded firewall scenarios
* Packet capture examples with tcpdump
