 FOOTPRINTING-AND-RECONNAISSANCE-ATTACKS-WITH-MULTIPLE-KALI-TOOLS-AND-NETWORK-SCANNING-WITH-ZENMAP


Cybersecurity Internship Program — NETWORKWALKS




| Field | Detail |
| :--- | :--- |
| **Pentester Name (Cybersecurity Professional)** | Precious Doowuese Dagba |
| **Program/Batch** | Cybersecurity Internship Program — Networkwalks |
| **Date** | 13 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools) and W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (`networkwalks.com`, the target assigned in the module instructions), 2. My own local lab network (`10.0.0.0/24`) |
| **Permission secured from client?** | Yes |
| **Phases covered** | Phase 1: Reconnaissance & Footprinting, Phase 2: Scanning & Network Discovery, Phase 3–5: In Progress |


---

1. LIABILITY DISCLAIMER

All activities documented in this report were carried out for educational purposes within the scope of authorised cybersecurity exercises. I performed the assessment against the specified domain with permission and conducted the internal network scans within my own virtualised lab environment.

The commands, tools and findings presented here are intended to demonstrate practical cybersecurity knowledge and responsible security testing. They should not be used against systems or networks without proper authorisation.

I understand that unauthorised access to computer systems and networks can have serious legal and professional consequences. All activities described in this report were undertaken with respect for applicable laws and ethical hacking principles.

2. INTRODUCTION

Week 2 of my Cybersecurity Internship at Networkwalks was centred on two important areas of practical cybersecurity: footprinting and reconnaissance, followed by network scanning and discovery.

I worked on two project modules: W2-PM1, which involved investigating the publicly available information associated with networkwalks.com using different Kali Linux tools, and W2-PM5, which focused on discovering active devices, identifying IP and MAC addresses, and generating a network topology using Zenmap and Nmap.

For the first module, I worked with six reconnaissance tools: WHOIS, WhatWeb, nslookup, curl, wafw00f and dnsrecon. Each tool helped me understand a different aspect of the target domain, including its registration details, hosting information, web technologies, DNS configuration, HTTP response headers and firewall protection.

The second module introduced me to practical network discovery. I initially attempted to perform the scan from my Windows host using Zenmap, but I encountered issues with host discovery and MAC address identification. Rather than proceeding with incomplete results, I investigated the network configuration and eventually moved the scanning activity into my Kali Linux virtual machine.

Working within my VirtualBox lab environment, I verified the network interface, checked the IP configuration and performed a Ping Scan on the 10.0.0.0/24 subnet.

This project gave me an opportunity to move beyond simply learning what cybersecurity tools do and actually use them, examine their outputs, troubleshoot unexpected behaviour and understand the networking concepts behind the results.

## 3. TOOLS AND TECHNOLOGIES USED

The following tools and environments were used throughout the two modules.

| Tool / Environment | Purpose |
| :--- | :--- |
| **Kali Linux** | Operating system used for the reconnaissance exercises and internal network scanning. |
| **Oracle VM VirtualBox** | Provided the virtualised environment for running Kali Linux and configuring the internal lab network. |
| **Windows 11** | Host operating system used for managing the virtual machine and initially attempting the Zenmap scan. |
| **WHOIS** | Retrieved publicly available domain registration information, registrar details and name servers. |
| **WhatWeb** | Identified technologies and software associated with the target website. |
| **nslookup** | Resolved the domain name to its corresponding IP address. |
| **curl** | Retrieved HTTP response headers from the target website. |
| **wafw00f** | Checked for and identified Web Application Firewall protection. |
| **dnsrecon** | Enumerated publicly available DNS records. |
| **Zenmap** | Provided a graphical interface for configuring and viewing Nmap scans. |
| **Nmap** | Performed host discovery across the internal lab subnet. |
| **iproute2 (`ip addr show`)** | Helped me inspect the network interfaces and IP configuration of my Kali VM. |
| **Windows Command Prompt (`ipconfig`)** | Used to inspect the Windows host's network configuration. |


4. ACTIVITIES PERFORMED

4.1 W2-PM1: FOOTPRINTING AND RECONNAISSANCE USING KALI LINUX

The first module introduced me to the information-gathering stage of ethical hacking.

My task was to investigate networkwalks.com using six Kali Linux tools and document the information returned by each one.

I carried out the following activities.

4.1.1 WHOIS – Domain Registration Lookup

I started with WHOIS to retrieve the publicly available registration information associated with networkwalks.com.

Command executed:

```bash
whois networkwalks.com
```





The output provided information about the domain registrar, registration and expiry dates, domain status and authoritative name servers.

Some of the details I identified were:

- Registrar: GoDaddy.com, LLC
- Creation Date: 6 November 2019
- Expiry Date: 6 November 2027
- Name Server 1: NS6135.HOSTGATOR.COM
- Name Server 2: NS6136.HOSTGATOR.COM

This exercise helped me understand how domain registration information can reveal details about the organisations and infrastructure associated with a website.

4.1.2 WhatWeb – Website Technology Fingerprinting

Next, I used WhatWeb to identify the technologies running on the target website.

Command executed:

whatweb networkwalks.com

