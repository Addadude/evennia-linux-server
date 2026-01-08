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

  


