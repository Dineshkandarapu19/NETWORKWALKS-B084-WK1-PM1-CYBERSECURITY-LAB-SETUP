# PENETRATION TESTING REPORT
## Footprinting & Network Scanning Phases

**Project:** W2-PM-FINAL — Cybersecurity Internship  
**Organization:** NetworkWalks  
**Prepared by:** Kandharapu Dinesh  
**Program:** NetworkWalks Cybersecurity Internship  
**Assessment period:** 11–12 November 2026  
**Modules documented:** W2-PM1 (Footprinting with Multiple Kali Tools) and W2-PM5 (Network Scanning with Zenmap)  
**Targets assessed:** `networkwalks.com` (passive / limited service identification) and the authorized local network `192.168.1.0/24`  
**Assessment type:** Educational security assessment and network discovery

---

## 1. Liability Disclaimer

This report documents the commands executed and the outputs observed during the assigned educational cybersecurity activities. The results represent the state of the target and local network at the time of testing and may change.

Website reconnaissance was limited to the listed information-gathering commands. Network discovery was performed against the local subnet `192.168.1.0/24`. No exploitation, password attacks, denial-of-service testing, or attempts to access private data are represented in this report.

Testing must only be performed on systems and networks for which explicit authorization has been granted. The observations below are not, by themselves, proof of exploitable vulnerabilities.

## 2. Introduction

The purpose of this assessment was to practise two phases of a basic penetration-testing workflow:

1. **Footprinting and reconnaissance (W2-PM1):** collect publicly available domain, DNS, web-technology, HTTP-response, and web-application-firewall information for `networkwalks.com`.
2. **Network scanning (W2-PM5):** use Zenmap/Nmap to identify active hosts on the local IPv4 subnet, record available IP and MAC address information, and view the discovered hosts in a network topology.

The report records the commands, selected output, interpretation, and screenshot evidence for each activity.

## 3. Tools Used

| Tool | Purpose |
|---|---|
| WHOIS | Retrieve public domain registration information |
| WhatWeb | Identify web technologies and server/application fingerprints |
| Nslookup | Query DNS records and resolve a domain name |
| cURL | Inspect HTTP response headers |
| WAFW00F | Identify a web application firewall when detectable |
| DNSRecon | Enumerate publicly discoverable DNS records |
| Zenmap / Nmap | Discover live hosts on the local subnet and display host details/topology |

## 4. Activities Performed

### 4.1 Footprinting and Reconnaissance — W2-PM1

The following commands were executed from the Kali Linux terminal against `networkwalks.com`.

#### 4.1.1 WHOIS lookup

**Command**
```bash
whois networkwalks.com
```

**Selected output**
```text
Domain Name: NETWORKWALKS.COM
Registrar: GoDaddy.com, LLC
Registrar WHOIS Server: whois.godaddy.com
Creation Date: 2025-11-12T10:08:43Z
Updated Date: 2025-11-12T10:08:43Z
Registry Expiry Date: 2027-11-06T22:51:46Z
Name Server: NS6135.HOSTGATOR.COM
Name Server: NS6136.HOSTGATOR.COM
DNSSEC: unsigned
```

**Observation**

The WHOIS response identifies GoDaddy.com, LLC as the registrar and lists two HostGator nameservers. The displayed DNSSEC status is `unsigned`. Registration details and dates are public domain metadata; the unsigned status is an item that the domain owner may review against its DNS security requirements. It is not proof of a compromise.

**Evidence:** [`01-whois-networkwalks.png`](Screenshots/01-whois-networkwalks.png)

#### 4.1.2 Web technology identification with WhatWeb

**Command**
```bash
whatweb networkwalks.com
```

**Selected output**
```text
http://networkwalks.com [301 Moved Permanently]
  Apache
  IP[192.232.216.135]

https://networkwalks.com [200 OK]
  Apache
  Bootstrap[7.1.4]
  JQuery[3.7.1]
  MetaGenerator[WordPress 7.1.4]
  Title[NetworkWalks Academy]
  Email[info@networkwalks.com]
  Country[UNITED STATES]
```

**Observation**

The HTTP endpoint redirects to HTTPS, and the HTTPS endpoint returns `200 OK`. WhatWeb identifies Apache, WordPress, Bootstrap, and jQuery. Technology fingerprinting can help defenders maintain and patch exposed software. Version strings reported by fingerprinting tools should be verified against the actual installed versions before making a vulnerability determination.

**Evidence:** [`02-whatweb-networkwalks.png`](Screenshots/02-whatweb-networkwalks.png)

#### 4.1.3 DNS lookup with Nslookup

**Command**
```bash
nslookup networkwalks.com
```

**Selected output**
```text
Server:         8.8.8.8
Address:        8.8.8.8#53

Non-authoritative answer:
Name:   networkwalks.com
Address: 192.232.216.135
```

**Observation**

The DNS resolver used was `8.8.8.8`. The queried domain resolved to IPv4 address `192.232.216.135`. A non-authoritative answer means the response was provided by the configured recursive resolver rather than directly by an authoritative nameserver.

#### 4.1.4 HTTP header inspection with cURL

**Command**
```bash
curl -I https://networkwalks.com
```

**Selected output**
```text
HTTP/2 200
server: Apache
content-type: text/html; charset=UTF-8
x-nginx-cache: WordPress
referrer-policy: no-referrer-when-downgrade
```

**Observation**

The HTTPS request returned `HTTP/2 200`, indicating a successful response to the HEAD request. The response identifies Apache and an HTML content type. The captured headers also include a referrer policy and an `x-nginx-cache` header. This is a limited header sample; a complete security-header review would require checking the full response and comparing it with the site's intended policy.

**Evidence for Nslookup and cURL:** [`03-nslookup-and-curl.png`](Screenshots/03-nslookup-and-curl.png)

#### 4.1.5 Web Application Firewall detection with WAFW00F

**Command**
```bash
wafw00f networkwalks.com
```

**Selected output**
```text
[*] Checking https://networkwalks.com
[+] The site https://networkwalks.com is behind ModSecurity (SpiderLabs) WAF.
[~] Number of requests: 2
```

**Observation**

WAFW00F identified a ModSecurity (SpiderLabs) web application firewall signature after two requests. This indicates that a WAF was detectable during this test. It does not establish that every attack is blocked or that the configuration is effective.

**Evidence:** [`04-wafw00f.png`](Screenshots/04-wafw00f.png)

#### 4.1.6 DNS enumeration with DNSRecon

**Command**
```bash
dnsrecon -d networkwalks.com
```

**Selected output**
```text
INFO Starting enumeration for domain: networkwalks.com
ERROR No answer for DNSSEC query for networkwalks.com
INFO SOA ns6135.hostgator.com 50.87.144.87
INFO NS ns6135.hostgator.com 50.87.144.87
INFO NS ns6136.hostgator.com 192.232.216.131
INFO MX mail.networkwalks.com 192.232.216.135
INFO A networkwalks.com 192.232.216.135
INFO TXT networkwalks.com v=spf1 +a +mx +ip4:50.87.144.87 +include:websitewelcome.com ~all
INFO Enumerating SRV Records
INFO 8 Records Found
INFO Completed enumeration for domain: networkwalks.com
```

**Observation**

DNSRecon reported the SOA and NS records, an MX record, an A record, a TXT/SPF record, and SRV autodiscover records. It reported eight records found. The DNSSEC query returned no answer, consistent with the WHOIS result showing DNSSEC as unsigned. The SPF TXT record lists permitted sending sources; the domain owner should periodically review whether these entries still match its mail infrastructure.

**Evidence:** [`05-dnsrecon.png`](Screenshots/05-dnsrecon.png)

### 4.2 Network Scanning with Zenmap — W2-PM5

#### 4.2.1 Zenmap interface

Zenmap was opened on the Windows host and used as the graphical interface for Nmap scanning.

**Evidence:** [`06-zenmap-interface.png`](Screenshots/06-zenmap-interface.png)

#### 4.2.2 Local subnet discovery

**Target**
```text
192.168.1.0/24
```

**Nmap command shown by Zenmap**
```bash
nmap -sn 192.168.1.0/24
```

**Selected output**
```text
Nmap scan report for 192.168.1.1
Host is up (0.12s latency).
MAC Address: C4:9A:31:5C:C5:D8 (Zyxel Communications)

Nmap scan report for IPC_2117 (192.168.1.3)
Host is up (0.12s latency).
MAC Address: 5C:35:48:88:F3:C8 (Aditya Infotech)

Nmap scan report for moto-g04s (192.168.1.8)
Host is up (0.12s latency).
MAC Address: 2E:23:8E:76:02:FA (Unknown)

Nmap scan report for 192.168.1.14
Host is up (0.12s latency).
MAC Address: 62:A0:00:84:68:4F (Unknown)

Nmap scan report for 192.168.1.15
Host is up (0.13s latency).
MAC/vendor line is visible in the screenshot, but the displayed MAC value appears incomplete; verify it from the original scan before recording the full address.

Nmap scan report for host.docker.internal (192.168.1.10)
Host is up.

Nmap done: 256 IP addresses (6 hosts up) scanned in 9.24 seconds
```

**Observation**

The ping scan checked all 256 addresses in the `/24` subnet and identified **six live hosts**. Four entries display complete MAC addresses in the captured text. The `192.168.1.15` MAC/vendor line appears incomplete in the screenshot and should be verified from the original scan; the `host.docker.internal` entry did not show a MAC address. Vendor identification is based on the MAC address prefix and may be unknown or approximate. A ping scan identifies responsive hosts; it does not perform a full port or vulnerability assessment.

**Evidence:** [`07-zenmap-ping-scan-output.png`](Screenshots/07-zenmap-ping-scan-output.png)

#### 4.2.3 Host details

The Zenmap Host Details view was opened for `192.168.1.1`.

**Selected details**
```text
Host: 192.168.1.1
State: up
Open ports: 0
Filtered ports: 0
Closed ports: 0
Scanned ports: 0

IPv4: 192.168.1.1
MAC: C4:9A:31:5C:C5:D8
```

**Observation**

The selected host was reachable and identified as `192.168.1.1`. The Host Details panel displayed its MAC address. Since this was a ping scan (`-sn`), no TCP/UDP port scan was performed; the zero port counts must not be interpreted as proof that the device has no open services.

**Evidence:** [`08-zenmap-host-details.png`](Screenshots/08-zenmap-host-details.png)

#### 4.2.4 Network topology

Zenmap's Topology tab displayed the six discovered hosts around the scanning host.

**Observation**

The topology view provides a visual representation of the responsive devices detected on the local subnet. It helps communicate the discovered network layout, but the diagram does not establish the physical network connections between devices.

**Evidence:** [`09-zenmap-network-topology.png`](Screenshots/09-zenmap-network-topology.png)

## 5. Risk Analysis and Impact

The following table records observations and suggested defensive considerations. These are not confirmed vulnerabilities.

| No. | Observation | Potential impact / consideration | Suggested priority |
|---:|---|---|---|
| 1 | WHOIS and DNS metadata are publicly discoverable | Public metadata can support reconnaissance and infrastructure mapping | Informational |
| 2 | WHOIS reports DNSSEC as unsigned; DNSRecon received no DNSSEC answer | DNS responses do not have DNSSEC validation protection for this domain as observed | Review |
| 3 | WhatWeb fingerprinted Apache, WordPress, Bootstrap, and jQuery | Public technology/version fingerprints can help an attacker identify software to investigate | Review patch status |
| 4 | WAFW00F detected ModSecurity (SpiderLabs) | A WAF is present/detectable, but its effectiveness was not tested | Informational |
| 5 | DNS records expose mail, nameserver, and service-discovery information | These records reveal parts of the public infrastructure; ensure records are intentional | Informational |
| 6 | Six live devices responded on `192.168.1.0/24` | Unmanaged or unnecessary devices can increase the local attack surface | Review inventory |
| 7 | Zenmap ping scan did not inspect ports | Service exposure remains undetermined by this scan | Further authorized assessment required |

## 6. Recommendations

1. **DNS security:** Review DNSSEC support with the DNS provider and enable signing/validation if supported and appropriate.
2. **Software maintenance:** Verify actual Apache, WordPress, Bootstrap, and jQuery versions and apply supported security updates.
3. **HTTP security headers:** Review the complete HTTPS response and configure headers such as Content-Security-Policy, Strict-Transport-Security, X-Content-Type-Options, and an appropriate Referrer-Policy according to application compatibility.
4. **WAF management:** Keep ModSecurity rules updated, monitor WAF logs, and periodically validate rules using approved test cases.
5. **DNS hygiene:** Review A, MX, TXT, NS, and SRV records; remove stale records and keep SPF/DKIM/DMARC policies aligned with the mail service.
6. **Local network inventory:** Identify the owner and purpose of each of the six discovered devices and remove or isolate unauthorized devices.
7. **Further testing:** If explicitly authorized, perform a separate, scoped service/port assessment. The current `-sn` scan did not enumerate ports.
8. **Documentation:** Retain scan dates, exact targets, commands, and evidence so future assessments can be compared consistently.

## 7. Conclusion

The W2-PM1 activities gathered public domain and DNS information, identified visible web technologies, inspected an HTTPS response, and detected a ModSecurity (SpiderLabs) WAF signature. The W2-PM5 Zenmap ping scan examined `192.168.1.0/24` and found six live hosts, with five MAC addresses shown in the captured output. Host details and a topology view were also recorded.

The activities provided practical experience with reconnaissance, DNS enumeration, HTTP inspection, WAF identification, and local network discovery. The results are observations from the captured assessment period and should not be treated as confirmation of exploitable vulnerabilities.

## 8. Evidence Collected

All evidence images are stored in the `Screenshots/` directory and embedded below.

| Evidence | Screenshot |
|---|---|
| WHOIS lookup | ![WHOIS output](Screenshots/01-whois-networkwalks.png) |
| WhatWeb fingerprint | ![WhatWeb output](Screenshots/02-whatweb-networkwalks.png) |
| Nslookup and cURL | ![Nslookup and cURL output](Screenshots/03-nslookup-and-curl.png) |
| WAFW00F detection | ![WAFW00F output](Screenshots/04-wafw00f.png) |
| DNSRecon enumeration | ![DNSRecon output](Screenshots/05-dnsrecon.png) |
| Zenmap interface | ![Zenmap interface](Screenshots/06-zenmap-interface.png) |
| Zenmap ping scan | ![Zenmap ping scan](Screenshots/07-zenmap-ping-scan-output.png) |
| Zenmap host details | ![Zenmap host details](Screenshots/08-zenmap-host-details.png) |
| Zenmap topology | ![Zenmap topology](Screenshots/09-zenmap-network-topology.png) |

## Author and Project Information

**Prepared by:** Kandharapu Dinesh  
**Project:** W2-PM-FINAL — Penetration Testing Report  
**Organization:** NetworkWalks  
**Modules:** W2-PM1 and W2-PM5  
**Environment:** Kali Linux and Windows with Zenmap/Nmap  
**Report format:** Markdown with supporting screenshot evidence

---

*End of Report*
