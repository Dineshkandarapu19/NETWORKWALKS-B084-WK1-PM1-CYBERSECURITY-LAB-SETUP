# Week 02 – Project Module 1: Footprinting Using Multiple Kali Tools

## Project Overview

This practical focuses on performing website footprinting and reconnaissance using six different tools available in Kali Linux.

The objective is to understand how publicly accessible domain registration information, DNS records, web technologies, HTTP response headers, and Web Application Firewall (WAF) information can be identified during the reconnaissance phase of a penetration testing workflow.

**Internship:** NetworkWalks
**Week:** 02
**Project Module:** W2-PM1
**Category:** Cybersecurity & Ethical Hacking
**Environment:** Kali Linux (VirtualBox)
**Target Domain:** `networkwalks.com`

---

## Objectives

- Retrieve publicly available domain registration information.
- Identify technologies used by a website.
- Understand DNS resolution and domain-to-IP mapping.
- Inspect HTTP response headers.
- Identify the presence of a Web Application Firewall.
- Enumerate publicly available DNS records.

## Tools & Technologies Used

| Tool       | Purpose                            |
| ---------- | ---------------------------------- |
| WHOIS      | Domain registration lookup         |
| WhatWeb    | Website technology fingerprinting  |
| Nslookup   | DNS resolution                     |
| cURL       | HTTP response header inspection    |
| Wafw00f    | Web Application Firewall detection |
| DNSRecon   | DNS record enumeration             |
| Kali Linux | Testing environment                |
| VirtualBox | Virtualization platform            |

---

## 🔬 Practical Implementation

### 1. WHOIS – Domain Registration Lookup

**Command:**

```bash
whois networkwalks.com
```

**Observations:**

- Registrar: GoDaddy.com, LLC
- Domain creation: 06 November 2019
- Registry expiry: 06 November 2027
- Name servers: NS6135.HOSTGATOR.COM and NS6136.HOSTGATOR.COM
- DNSSEC: Unsigned

**Outcome:** Retrieved publicly available domain registration and name server information.

**Screenshot:**
<img width="1920" height="982" alt="01-whois-networkwalks" src="https://github.com/user-attachments/assets/b11fff24-84b1-418b-9a74-ea199f2d1cb2" />


---

### 2. WhatWeb – Website Technology Fingerprinting

**Command:**

```bash
whatweb networkwalks.com
```

**Observations:**

- Web Server: Apache
- CMS: WordPress 7.1.4 (as reported by WhatWeb)
- Bootstrap: 7.1.4 (as reported by WhatWeb)
- jQuery: 3.7.1
- WordPress Download Manager: 3.3.76
- Website IP: 192.232.216.135
- HTTP Status: 200 OK

**Outcome:** Identified technologies and publicly exposed website information through web fingerprinting.

**Screenshot:**

<img width="1920" height="982" alt="02-whatweb-networkwalks" src="https://github.com/user-attachments/assets/28564780-3560-43b9-aa73-687a96d06cbf" />


---

### 3. Nslookup – DNS Resolution

**Command:**

```bash
nslookup networkwalks.com
```

**Observations:**

- DNS Resolver: 8.8.8.8 (Google Public DNS)
- DNS Port: 53
- Domain: networkwalks.com
- Resolved IPv4 Address: 192.232.216.135
- Response Type: Non-authoritative answer

**Outcome:** Successfully resolved the domain name into its corresponding IPv4 address.

**Screenshot:**

<img width="1920" height="982" alt="03-nslookup-and-curl" src="https://github.com/user-attachments/assets/32826781-5afa-4481-8d11-71071e5c305b" />


---

### 4. cURL – HTTP Response Header Inspection

**Command:**

```bash
curl -I https://networkwalks.com
```

**Observations:**

- HTTP Status: 200 OK
- Server: Apache
- Content-Type: text/html; charset=UTF-8
- Referrer-Policy: no-referrer-when-downgrade
- WordPress REST API reference: /wp-json/
- Cookie attributes: Secure and HttpOnly

**Outcome:** Inspected HTTP response headers to understand server information, response status, cookie attributes, and website configuration.

**Screenshot:**
<img width="1920" height="982" alt="03-nslookup-and-curl" src="https://github.com/user-attachments/assets/589210fa-4228-4acd-aafd-dcdbb1844f8f" />


---

### 5. Wafw00f – Web Application Firewall Detection

**Command:**

```bash
wafw00f networkwalks.com
```

**Observations:**

- WAF Detection: Successful
- Identified WAF: ModSecurity (SpiderLabs)
- Number of Requests: 2

**Outcome:** Identified a Web Application Firewall associated with the target website.

**Screenshot:**
<img width="1920" height="982" alt="04-wafw00f" src="https://github.com/user-attachments/assets/fe7c017c-99fe-4f8a-9689-bb47fbb38bae" />


---

### 6. DNSRecon – DNS Enumeration

**Command:**

```bash
dnsrecon -d networkwalks.com -t std
```

**Observations:**

- SOA Record: ns6135.hostgator.com
- Name Servers: ns6135.hostgator.com and ns6136.hostgator.com
- A Record: 192.232.216.135
- MX Record: mail.networkwalks.com
- TXT Records: SPF and Google site verification
- SRV Records: Autodiscover services
- Total Records Found: 8
- DNSSEC Query: No answer returned

**Outcome:** Retrieved publicly available DNS records and identified domain-related DNS infrastructure information.

**Screenshot:**

<img width="1920" height="982" alt="05-dnsrecon" src="https://github.com/user-attachments/assets/927392f7-62ce-4615-bf46-4ae705e1595d" />


---

## 📊 Summary of Findings

| Practical | Result                                     |
| --------- | ------------------------------------------ |
| WHOIS     | GoDaddy registrar identified               |
| WhatWeb   | Apache and WordPress technologies detected |
| Nslookup  | Domain resolved to 192.232.216.135         |
| cURL      | HTTP 200 OK response received              |
| Wafw00f   | ModSecurity WAF detected                   |
| DNSRecon  | 8 DNS records found                        |

## 🔐 Security Relevance

Website footprinting and reconnaissance help cybersecurity professionals understand publicly exposed information about a target domain before conducting further security assessments.

The practical demonstrated how different tools can be used to gather information about domain registration, DNS infrastructure, web technologies, HTTP configurations, and security mechanisms.

The collected information represents reconnaissance observations and does not independently establish the presence of exploitable vulnerabilities.

## 📚 Key Learnings

Through this practical, I gained hands-on experience with:

- Domain registration and WHOIS queries.
- Website technology fingerprinting.
- DNS resolution and DNS record types.
- HTTP response headers and cookie security attributes.
- Web Application Firewall identification.
- DNS enumeration using Kali Linux tools.
- Capturing and organizing technical evidence.

## ⚠️ Disclaimer

This practical was performed as part of the NetworkWalks cybersecurity internship within the authorized internship scope.

All activities were intended for educational purposes and passive reconnaissance. No exploitation or unauthorized access was performed.

---

**Internship:** NetworkWalks
**Project:** Week 02 – PM1 Footprinting with Multiple Kali Tools
**Status:** Completed
