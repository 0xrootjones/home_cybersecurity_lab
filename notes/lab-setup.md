Home Cybersecurity Lab – Setup Notes

**This document outlines the components and configuration of my personal cybersecurity home lab, designed to simulate a small-scale SOC (Security Operations Center) environment for practicing detection, monitoring, and response.

---

Infrastructure Overview

- Proxmox VE – Bare-metal hypervisor hosting the full lab stack  
- pfSense – Virtualized firewall with VLAN support, NAT, and VPN  
- AdGuard Home – DNS filtering for ads and trackers  
- Wazuh – SIEM server on Ubuntu 22.04  
- Sysmon – Logging agent on Windows 10 VM  
- Windows 10 VM – Used to simulate endpoints and user behavior  
- Mac Mini – Additional endpoint for cross-platform testing

---

Network Design

 [WAN]
      |
    [pfSense VM]
      ├── VLAN 10: Internal LAN (Ubuntu + Windows)
      ├── VLAN 20: Secure Admin Zone
      └── VLAN 30: DNS Filtering Zone (AdGuard)

- pfSense assigns IP addresses via DHCP on each VLAN  
- VLAN 10 is used for general endpoint traffic (Windows and Ubuntu VMs)  
- VLAN 20 is reserved for management interfaces (Proxmox, Wazuh, etc.)  
- VLAN 30 routes traffic through AdGuard Home for DNS-level filtering  
- Inter-VLAN traffic is restricted via pfSense firewall rules  
- Syslog and Wazuh agents forward logs to the SIEM over secure channels

---

Lab Goals

- Learn SIEM fundamentals and endpoint monitoring  
- Build and test custom detection rules using Sysmon  
- Harden firewall rules and simulate segmentation  
- Use Obsidian.md to document workflows and detections  
- Eventually script routine checks and alerts

---

Current Status

- [x] pfSense installed with multi-VLAN config  
- [x] AdGuard running and filtering DNS  
- [x] Wazuh installed on Ubuntu + Windows agent deployed  
- [ ] Create and test custom detection rules  
- [ ] Enable alert forwarding to external system (email/webhook)

---

Tools Used

- Proxmox VE  
- pfSense  
- AdGuard Home  
- Wazuh  
- Sysmon  
- Obsidian.md  
- VS Code  
- Windows 10, Ubuntu 22.04, macOS

---

Next Steps

- Forward logs from macOS (via syslog or other agent)  
- Build test PowerShell-based attack to trigger Wazuh alerts  
- Document detection logic in Obsidian and upload samples
