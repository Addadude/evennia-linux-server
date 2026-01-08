# linux-networking-labs
This project documents the deployment and administration of a Linux-based multi-user Evennia MUD server. The goal was to gain hands-on experience with Linux system administration, networking, and basic security controls.
## Architecture

[Internet]
    |
[Router / NAT]
    |  (Port Forwarding)
[Firewall (iptables/firewalld)]
    |
[Debian Linux Server]
    |-- Evennia (Python venv)
    |-- Telnet Service
    |-- Web Client

## Key Configuration Areas
- Linux user and permission management
- Python virtual environments
- SSH key-based authentication
- Firewall rules using iptables/firewalld
- LAN and WAN port forwarding
- Service monitoring and log analysis

## Security Considerations
- Disabled password-based SSH authentication
- Restricted administrative access by IP
- Allowed only required ports through firewall
- Monitored logs using journalctl

## Troubleshooting Highlights
- Diagnosed wireless firmware issues on Debian systems
- Used dmesg and journalctl to identify driver loading errors
- Verified network connectivity and port accessibility across devices

## Lessons Learned
- Importance of firewall rule order
- How NAT affects service exposure
- Value of methodical troubleshooting and documentation
