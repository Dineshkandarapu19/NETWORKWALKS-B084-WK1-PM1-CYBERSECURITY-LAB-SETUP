# PENETRATION TESTING REPORT
## FOOTPRINTING & NETWORK SCANNING PHASES

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Project Information | Details |
|---|---|
| Pentester Name | Kandharapu Dinesh |
| Program/Batch | NetworkWalks Cybersecurity Internship |
| Date | [Enter submission date] |
| Modules Completed | W2-PM1 (Multiple Kali Tools), W2-PM5 (Zenmap Scanning) |
| Client/Target | networkwalks.com and my own local LAN |
| Permission | Activities performed within the assigned internship scope |
| Phases Covered | Phase 1: Reconnaissance & Footprinting; Phase 2: Scanning & Network Discovery |

---

## 1. Liability Disclaimer

I performed these activities only on the assigned target within the authorized internship scope and on my own local network. These activities are intended for educational and research purposes only.

Unauthorized access or misuse of cybersecurity tools may have legal consequences. All testing must be performed with appropriate authorization.

## 2. Introduction

This report documents the Week 2 activities completed during my NetworkWalks Cybersecurity Internship.

The report covers two practical modules:

- **W2-PM1:** Footprinting with Multiple Kali Linux Tools.
- **W2-PM5:** Network Scanning with Zenmap.

The footprinting activity involved gathering publicly available information about networkwalks.com using Kali Linux tools. The network scanning activity involved discovering live hosts and examining network information using Zenmap on my local network.

Each activity includes its objective, commands or procedures, observations, screenshots and security relevance.

## 3. Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Operating system for footprinting |
| WHOIS | Obtain domain registration information |
| WhatWeb | Identify website technologies |
| Nslookup | Resolve domain names using DNS |
| cURL | Inspect HTTP response headers |
| WAFW00F | Identify Web Application Firewall information |
| DNSRecon | Enumerate DNS records |
| Zenmap | Discover live hosts and scan networks |
| Windows CMD | Identify local IP and network configuration |

## 4. Activities Performed

### 4.1 Footprinting & Reconnaissance – W2-PM1

I performed footprinting against the assigned networkwalks.com target using six Kali Linux tools.

**1. WHOIS**

- Objective: Obtain publicly available domain registration information.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `01-whois networkwalks.png`

**2. WhatWeb**

- Objective: Identify technologies used by the target website.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `02-whatweb networkwalks.png`

**3. Nslookup**

- Objective: Resolve the domain name and identify its IP address.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `03-nslookup networkwalks.png`

**4. cURL**

- Objective: Inspect HTTP response headers.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `04-curl networkwalks.png`

**5. WAFW00F**

- Objective: Identify whether a Web Application Firewall protects the website.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `05-wafw00f networkwalks.png`

**6. DNSRecon**

- Objective: Enumerate available DNS records and related information.
- Command: `[Insert command used]`
- Observation: `[Insert your actual result]`
- Evidence: `06-dnsrecon networkwalks.png`

### 4.2 Network Scanning with Zenmap – W2-PM5

For the second activity, I used Zenmap to perform network discovery on my local LAN.

The practical involved identifying the local IP address and subnet, discovering live hosts, recording IP and MAC addresses, and generating a network topology.

**Step 1: Zenmap Installation**

Installed Zenmap on the Windows PC.

Evidence: `01-zenmap-installation.png`

**Step 2: Identify Local IP and Subnet**

Used the Windows `ipconfig` command to identify the local network configuration.

- Local IP: `[Insert actual IP]`
- Subnet Mask: `[Insert actual subnet mask]`
- Default Gateway: `[Insert actual gateway]`
- Network Subnet: `[Insert actual subnet]`

Evidence: `02-ipconfig.png`

**Step 3: Discover Live Hosts**

Performed a Ping Scan in Zenmap to discover active hosts on the local network.

- Scan Target: `[Insert actual subnet]`
- Total Live Hosts: `[Insert actual count]`

Evidence: `03-ping-scan.png`

**Step 4: Host Details**

Recorded the IP addresses and MAC addresses of discovered live hosts.

| No. | IP Address | MAC Address |
|---|---|---|
| 1 | [Actual IP] | [Actual MAC] |
| 2 | [Actual IP] | [Actual MAC] |
| 3 | [Actual IP] | [Actual MAC] |

Add or remove rows according to your actual scan results.

Evidence: `04-host-details.png`

**Step 5: Network Topology**

Opened the Topology section in Zenmap, enabled the legend and generated the network topology.

The topology output was saved in PDF format.

Evidence: `05-network-topology.png`

Report: `[Network Topology PDF](./Reports/)`

## 5. Risk Analysis / Impact

The following table provides a framework for documenting potential risks observed during the activities.

| No. | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---|---|---|---|---|
| 1 | Web technology information exposed | [Actual WhatWeb finding] | May assist technology fingerprinting | [Level] |
| 2 | Server IP identifiable | [Actual Nslookup finding] | Provides information about network infrastructure | [Level] |
| 3 | HTTP technical information exposed | [Actual cURL finding] | May assist further enumeration | [Level] |
| 4 | WAF technology identifiable | [Actual WAFW00F finding] | Reveals information about security architecture | [Level] |
| 5 | DNS infrastructure information exposed | [Actual DNSRecon finding] | Helps build an infrastructure profile | [Level] |
| 6 | Multiple live hosts visible | [Actual Zenmap finding] | Unknown devices may require investigation | [Level] |

**Risk level key:** Critical / High / Medium / Low / Informational.

These observations should not automatically be treated as confirmed vulnerabilities. Further authorized security testing is required to validate actual security weaknesses.

## 6. Recommendations

Based on the observations from the footprinting and network scanning activities, the following improvements are recommended:

1. **Review publicly exposed technology information:** Regularly review the information exposed about website technologies and software.
2. **Keep software updated:** Maintain updated CMS platforms, plugins and web technologies.
3. **Review HTTP headers:** Check whether unnecessary technical information is exposed.
4. **Review DNS records:** Ensure that only required DNS records and services are publicly exposed.
5. **Configure and monitor the WAF:** Maintain appropriate WAF configuration and monitoring.
6. **Perform regular network discovery:** Periodically scan internal networks to identify active devices.
7. **Investigate unknown devices:** Verify unexpected devices discovered during network scanning.
8. **Maintain network documentation:** Keep network topology and device information updated.
9. **Perform authorized security testing:** Conduct reconnaissance and scanning only within an approved scope.

## 7. Conclusion

During Week 2 of my NetworkWalks Cybersecurity Internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

In W2-PM1, I used six Kali Linux tools: WHOIS, WhatWeb, Nslookup, cURL, WAFW00F and DNSRecon to gather information about the assigned target domain.

In W2-PM5, I used Zenmap to identify my local network configuration, discover live hosts, collect IP and MAC address information, and generate a network topology.

These activities helped me understand the importance of information gathering and network discovery in cybersecurity.

I also learned how to document technical observations, understand their possible security impact and recommend appropriate improvements.

All activities were performed within the assigned educational testing scope.

## 8. Evidences Collected

### W2-PM1 – Footprinting

Screenshots are maintained in:

`../W2-PM1 - Footprinting with Multiple Kali Tools/Screenshots/`

### W2-PM5 – Network Scanning

Screenshots are maintained in:

`../W2-PM5 - Network Scanning with Zenmap/Screenshots/`

Network topology PDF is maintained in:

`../W2-PM5 - Network Scanning with Zenmap/Reports/`

## Author

**Kandharapu Dinesh**  
Cybersecurity Intern – NetworkWalks

## Project Information

- Program: NetworkWalks Cybersecurity Internship
- Week: 02
- Project: W2-PM-FINAL
- Modules: W2-PM1 and W2-PM5
- Repository: GitHub
