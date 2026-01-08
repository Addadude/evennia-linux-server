# evennia-linux-server

Add project documentation for Linux-based Evennia server

# Troubleshooting Notes – Evennia Linux Server

This document captures real-world troubleshooting experiences while deploying and managing a Linux-based Evennia server. It highlights common issues, diagnostic methods, and solutions applied during the project.

---

## 📡 Networking Issues

<details>
<summary>WAN Connectivity Issues – Clients Could Not Connect</summary>

**Diagnosis:**
- Verified router port forwarding and NAT configuration
- Checked firewall rules on the Linux server
- Tested port accessibility from external devices using `nc` and `telnet`

**Solution:**
- Corrected router port forwarding for required service ports (Telnet, HTTP/HTTPS)
- Configured firewall to allow only required incoming ports
- Ensured Evennia server was listening on the correct network interfaces

</details>

<details>
<summary>NetworkManager Password Prompt Loop</summary>

**Diagnosis:**
- Repeated password prompts observed using `nmcli` logs
- Checked `wpa_supplicant` configuration
- Verified interface state with `ip a`

**Solution:**
- Ensured correct WiFi credentials and security settings
- Restarted NetworkManager service
- Brought interface up manually when needed

</details>

<details>
<summary>Wireless Driver / Firmware Issues</summary>

**Diagnosis:**
- Network interface showed `state DOWN` / `DORMANT`
- `dmesg` reported missing Broadcom firmware
- Required `.fw` files missing in `/lib/firmware`

**Solution:**
- Extracted Broadcom firmware using `b43-fwcutter`
- Copied files to `/lib/firmware/b43`
- Restarted network service and verified interface came online

- <

# OSI-Model-Cheat-Sheet

# OSI Model — Practical One-Page Cheat Sheet

A concise, hands-on reference for understanding and troubleshooting network connections using the **OSI (Open Systems Interconnection) model**. Designed for Linux system administration, networking labs, and interview preparation.

---

## Layer 7 — Application

**Purpose:** User-facing network services
**Key Question:** *Is the application itself working?*

**Examples**

* SSH, HTTP/HTTPS, FTP, DNS, Evennia

**Common Commands**

```bash
systemctl status <service>
journalctl -u <service>
curl http://localhost
ps aux | grep <service>
```

**Typical Failures**

* Service not running
* Application misconfiguration
* Crashes or runtime errors

---

## Layer 6 — Presentation

**Purpose:** Data formatting, encryption, encoding
**Key Question:** *Can data be securely and correctly understood?*

**Examples**

* TLS / SSL
* Encryption
* UTF-8 encoding

**Common Commands**

```bash
openssl s_client -connect host:443
ssh -vvv user@host
file <filename>
```

**Typical Failures**

* TLS handshake errors
* Cipher or protocol mismatch
* Garbled or unreadable data

---

## Layer 5 — Session

**Purpose:** Session establishment and persistence
**Key Question:** *Does the connection stay alive?*

**Examples**

* Login sessions
* Authentication state

**Common Commands**

```bash
ss -tan state established
who
w
```

**Typical Failures**

* Random disconnects
* Idle timeouts
* NAT session expiration

---

## Layer 4 — Transport

**Purpose:** Reliable delivery and port management
**Key Question:** *Is the port reachable and responding?*

**Examples**

* TCP / UDP
* Ports (22, 80, 443, 4000)

**Common Commands**

```bash
ss -tulnp
nc -zv host port
telnet host port
tcpdump -i eth0 port 4000
```

**Typical Failures**

* Port closed
* Firewall blocking traffic
* Service not listening

---

## Layer 3 — Network

**Purpose:** Logical addressing and routing
**Key Question:** *Can I reach the destination host?*

**Examples**

* IPv4 / IPv6
* Routing tables
* ICMP (ping)

**Common Commands**

```bash
ip addr
ip route
ping 8.8.8.8
traceroute example.com
```

**Typical Failures**

* No default gateway
* Incorrect subnet
* Routing loops or black holes

---

## Layer 2 — Data Link

**Purpose:** Local network delivery
**Key Question:** *Can I communicate on the local network?*

**Examples**

* Ethernet
* Wi-Fi
* MAC addresses
* ARP

**Common Commands**

```bash
ip neigh
arp -a
iw dev
bridge link
```

**Typical Failures**

* ARP resolution failures
* Wi-Fi association issues
* VLAN or switch misconfiguration

---

## Layer 1 — Physical

**Purpose:** Physical transmission of data
**Key Question:** *Is there a physical connection?*

**Examples**

* Network cables
* Network interface cards (NICs)
* Radio signals (Wi-Fi)

**Common Commands**

```bash
ip link
ethtool eth0
nmcli device status
```

**Typical Failures**

* Interface down
* No link light
* Bad cable or hardware failure

---

## Core Troubleshooting Rule

**Always troubleshoot from the bottom up (Layer 1 → Layer 7).**

> If a lower layer is failing, higher layers cannot function correctly.

---

## Professional Summary

> I use the OSI model to methodically troubleshoot networking issues, validating physical connectivity and link-layer communication first, then isolating routing, transport, session, encryption, and application-level failures.

---

*This cheat sheet is intended as a living document—update it with commands, notes, or examples from your own labs and production systems.*
