
# NETWORKWALKS-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

# Cybersecurity & Penetration Testing Internship

A practical cybersecurity internship repository documenting hands-on activities, lab configurations, reconnaissance techniques, network discovery, and penetration-testing fundamentals completed during the NetworkWalks Cybersecurity Internship.

**Internship Organization:** NetworkWalks  
**Internship Track:** Cybersecurity & Penetration Testing  
**Internship Batch:** B084  
**Intern:** Kandharapu Dinesh  

---

## Repository Overview

This repository contains the practical tasks and documentation completed during the internship.

The work focuses on developing foundational cybersecurity skills through hands-on exercises involving:

- Virtual penetration-testing lab setup
- Kali Linux configuration
- Network configuration and troubleshooting
- Footprinting and reconnaissance
- DNS enumeration
- Web technology identification
- Web Application Firewall detection
- Network scanning and host discovery
- Security observations and risk analysis

---

# Week 01 – Cybersecurity Lab Setup

**Project:** W2-WK1 PM1 – Cybersecurity Lab Setup  
**Status:** Completed

## Objective

To build and configure a virtual penetration-testing environment using Oracle VirtualBox and Kali Linux, including network connectivity, static IP addressing, DHCP configuration, and host-to-guest file sharing.

## Tools & Technologies

- Oracle VirtualBox
- Kali Linux
- NetworkManager
- NAT Networking
- DHCP
- Linux Terminal
- Windows 11

## Implementation Workflow

### 1. Virtual Machine Setup
- Installed and configured Kali Linux in VirtualBox.
- Prepared Kali Linux as the attacker environment.
- Configured the VM network adapter.

### 2. NAT Network Configuration
- Created a VirtualBox NAT Network.
- Configured subnet: `10.0.0.0/24`.
- Configured gateway: `10.0.0.1`.
- Enabled the DHCP server.

### 3. Static IP Configuration
- Assigned Kali Linux static IP: `10.0.0.2/24`.
- Configured gateway: `10.0.0.1`.
- Configured DNS: `8.8.8.8` and `1.1.1.1`.

### 4. DHCP Conflict Resolution
- Identified an IP address conflict.
- Changed DHCP server IP to `10.0.0.254`.
- Configured DHCP allocation range: `10.0.0.3–10.0.0.253`.
- Successfully resolved the IP conflict.

### 5. Shared Folder Configuration
- Configured Windows Downloads as a shared folder.
- Mounted the shared folder at `/downloads`.
- Enabled read/write access.
- Verified file creation from Kali Linux.

### 6. Clipboard and Drag-and-Drop
- Enabled bidirectional shared clipboard.
- Enabled bidirectional drag-and-drop.

### 7. Connectivity Testing
- Verified Kali network interface configuration.
- Tested external connectivity using ping.
- Verified internet access.

## Final Network Configuration

| Component | Configuration |
|---|---|
| Virtualization | Oracle VirtualBox |
| Operating System | Kali Linux |
| Network Mode | NAT Network |
| Subnet | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| Kali IP | 10.0.0.2/24 |
| DHCP Server | 10.0.0.254 |
| DHCP Range | 10.0.0.3–10.0.0.253 |
| DNS | 8.8.8.8, 1.1.1.1 |

## Key Outcomes
- Configured a Kali Linux attacker environment.
- Established NAT-based network connectivity.
- Implemented static IP addressing.
- Resolved DHCP-related IP conflicts.
- Established host-to-guest file sharing.
- Verified internet connectivity.

---

# Week 02 – Footprinting & Network Scanning

**Modules Completed:**
- W2-PM1 – Footprinting with Multiple Kali Tools (Elective)
- W2-PM5 – Network Scanning with Zenmap (Mandatory)
- W2-PM-FINAL – Penetration Testing Report (Mandatory)

**Status:** Completed

## Objective

To perform practical reconnaissance and network discovery using Kali Linux tools and Zenmap, collect publicly available information about a domain, identify web technologies, inspect DNS records, detect WAF signatures, and discover active hosts on a local network.

## Tools & Technologies

- Kali Linux
- WHOIS
- WhatWeb
- Nslookup
- cURL
- WAFW00F
- DNSRecon
- Zenmap
- Nmap
- Windows 11

## Module 1: Footprinting with Multiple Kali Tools (W2-PM1)

Performed reconnaissance against `networkwalks.com` using multiple information-gathering tools.

### 1. WHOIS
**Command:**
```bash
whois networkwalks.com
```
**Purpose:**
Collected public domain registration information, registrar details, registration dates, and nameservers.

**Observation:**
Identified GoDaddy as the registrar and HostGator nameservers.

### 2. WhatWeb
**Command:**
```bash
whatweb networkwalks.com
```
**Purpose:**
Identified publicly detectable web technologies and server information.

**Observation:**
Detected Apache, WordPress, Bootstrap, and jQuery. The HTTPS endpoint returned HTTP 200 OK.

### 3. Nslookup
**Command:**
```bash
nslookup networkwalks.com
```
**Purpose:**
Resolved the domain name and retrieved its IPv4 address.

**Observation:**
The domain resolved to `192.232.216.135` through the configured DNS resolver.

### 4. cURL
**Command:**
```bash
curl -I https://networkwalks.com
```
**Purpose:**
Inspected HTTP response headers from the HTTPS endpoint.

**Observation:**
Received HTTP/2 200 response and identified server and response-header information.

### 5. WAFW00F
**Command:**
```bash
wafw00f networkwalks.com
```
**Purpose:**
Identified whether a Web Application Firewall signature could be detected.

**Observation:**
Detected ModSecurity (SpiderLabs) WAF.

### 6. DNSRecon
**Command:**
```bash
dnsrecon -d networkwalks.com
```
**Purpose:**
Enumerated publicly discoverable DNS records.

**Observation:**
Identified SOA, NS, MX, A, TXT, and SRV records. DNSSEC query returned no answer.

## Module 2: Network Scanning with Zenmap (W2-PM5)

Performed local network discovery using Zenmap, the graphical interface for Nmap.

### Activities Performed

1. Installed and opened Zenmap on Windows.
2. Identified the local network subnet.
3. Performed a ping scan to discover active hosts.
4. Recorded discovered IP addresses.
5. Examined available MAC address and vendor information.
6. Reviewed host details.
7. Generated and examined the network topology view.

### Network Scanning Command

**Target subnet:**
```text
192.168.1.0/24
```

**Nmap command:**
```bash
nmap -sn 192.168.1.0/24
```

**Observation:**
- Scanned 256 IP addresses.
- Identified 6 live hosts.
- Recorded available MAC addresses and vendor information.
- Examined host details using Zenmap.
- Reviewed the discovered hosts through the topology view.

**Note:** The `-sn` option performs host discovery without a port scan.

## Key Outcomes
- Performed domain footprinting and reconnaissance.
- Retrieved domain registration and DNS information.
- Identified web technologies and server information.
- Inspected HTTPS response headers.
- Detected a ModSecurity WAF signature.
- Enumerated DNS records.
- Discovered six active hosts on the local subnet.
- Examined host details and network topology.

---

# Skills Developed

Through these two weeks of practical activities, I developed hands-on experience in:

- Linux environment configuration
- Virtual machine networking
- NAT and DHCP configuration
- Static IP addressing
- Network troubleshooting
- Domain footprinting
- DNS enumeration
- Web technology fingerprinting
- HTTP response inspection
- WAF detection
- Network host discovery
- Nmap and Zenmap usage
- Basic security observation and risk analysis
- Technical documentation and reporting

---

# Repository Structure

```text
NETWORKWALKS-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP/
│
├── README.md
│
├── week-01/
│   ├── README.md
│   └── WK1-PM1 - Cybersecurity Lab Setup/
│       ├── README.md
│       ├── Screenshots/
│       └── shared-folder-test.txt
│
└── week-02/
    ├── README.md
    │
    ├── W2-PM1 - Footprinting with Multiple Kali Tools/
    │   ├── README.md
    │   └── Screenshots/
    │
    ├── W2-PM5 - Network Scanning with Zenmap/
    │   ├── README.md
    │   ├── Screenshots/
    │   └── Reports/
    │
    └── W2-PM-FINAL - Penetration Testing Report/
        └── README.md
```

---

# Learning Journey & Next Steps

These activities provided practical exposure to cybersecurity lab configuration, reconnaissance, and network discovery.

**Upcoming learning goals:**
- Continue hands-on penetration-testing exercises.
- Explore vulnerability assessment techniques.
- Practise service and port enumeration in authorized environments.
- Improve network security analysis.
- Develop practical security assessment projects.

---

## Author

**Kandharapu Dinesh**  
Cybersecurity & Penetration Testing Intern  
NetworkWalks – Batch B084

**GitHub:** [DineshK1921](https://github.com/Dineshkandarapu19)

---

*Documenting my practical cybersecurity learning journey, one project at a time.*
