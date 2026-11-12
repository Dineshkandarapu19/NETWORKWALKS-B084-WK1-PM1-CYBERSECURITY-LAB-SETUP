# NETWORKWALKS-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

# Cybersecurity & Penetration Testing Lab Setup

## Week 1 – Internship Project

This repository documents my Week 1 cybersecurity internship task, focused on building a virtual penetration-testing lab environment using Oracle VirtualBox and Kali Linux.

## Objective

To configure a Kali Linux attacker machine with proper network connectivity, static IP addressing, DHCP support, and host-to-guest file sharing.

## Tools & Technologies

- Oracle VirtualBox
- Kali Linux
- NetworkManager
- NAT Networking
- DHCP
- Linux Terminal
- Windows 11 Host OS

## Lab Architecture

Windows Host Machine
        |
        |
   Oracle VirtualBox
        |
        |
     NAT Network
     10.0.0.0/24
        |
        |
     Kali Linux
     10.0.0.2/24

## Implementation Workflow

### 1. Virtual Machine Setup
- Installed and configured Kali Linux in VirtualBox.
- Prepared Kali Linux as the attacker environment.
- Configured VM network adapter.

### 2. NAT Network Configuration
- Created a VirtualBox NAT Network.
- Configured subnet: 10.0.0.0/24.
- Configured gateway: 10.0.0.1.
- Enabled DHCP server.

### 3. Static IP Configuration
- Configured Kali Linux with a static IPv4 address.
- Assigned IP: 10.0.0.2/24.
- Configured gateway: 10.0.0.1.
- Configured DNS: 8.8.8.8 and 1.1.1.1.

### 4. DHCP Conflict Resolution
- Identified an IP address conflict between Kali and the VirtualBox DHCP server.
- Discovered that the DHCP server was using 10.0.0.2.
- Changed DHCP server IP to 10.0.0.254.
- Configured DHCP allocation range:
  10.0.0.3 – 10.0.0.253.
- Successfully resolved the IP conflict.

### 5. Shared Folder Configuration
- Configured Windows Downloads as a shared folder.
- Mounted the shared folder at /downloads.
- Enabled read/write access.
- Verified file creation from Kali Linux.

### 6. Clipboard & Drag-and-Drop
- Enabled bidirectional shared clipboard.
- Enabled bidirectional drag-and-drop.

### 7. Connectivity Testing
- Verified Kali network interface.
- Tested external connectivity using ping.
- Verified internet access.

## Final Network Configuration

| Component | Configuration |
|---|---|
| Virtualization | Oracle VirtualBox |
| Operating System | Kali Linux |
| Network Mode | NAT Network |
| Network Subnet | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| Kali IP | 10.0.0.2/24 |
| DHCP Server | 10.0.0.254 |
| DHCP Range | 10.0.0.3–10.0.0.253 |
| DNS | 8.8.8.8, 1.1.1.1 |

## Key Outcomes

- Successfully configured a Kali Linux attacker environment.
- Established NAT-based network connectivity.
- Implemented static IP addressing.
- Enabled DHCP without IP conflicts.
- Troubleshot and resolved an IP address conflict.
- Established host-to-guest file sharing.
- Verified internet connectivity.

## Learning Outcomes

- Virtual machine networking.
- NAT and DHCP configuration.
- Static IP addressing.
- IP conflict troubleshooting.
- Linux network management.
- Shared folder configuration.
- Basic network connectivity testing.

## Next Steps

- Configure Windows victim machine.
- Configure Android victim environment.
- Connect all lab machines.
- Begin Week 2: Footprinting and Scanning.

---

**Internship Track:** Cybersecurity & Penetration Testing  
**Week:** 01  
**Status:** Kali attacker environment setup completed.
