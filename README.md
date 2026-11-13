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

3. TOOLS AND TECHNOLOGIES USED

The following tools and environments were used throughout the two modules.

Tool / Environment| Purpose
Kali Linux| Operating system used for the reconnaissance exercises and internal network scanning.
Oracle VM VirtualBox| Provided the virtualised environment for running Kali Linux and configuring the internal lab network.
Windows 11| Host operating system used for managing the virtual machine and initially attempting the Zenmap scan.
WHOIS| Retrieved publicly available domain registration information, registrar details and name servers.
WhatWeb| Identified technologies and software associated with the target website.
nslookup| Resolved the domain name to its corresponding IP address.
curl| Retrieved HTTP response headers from the target website.
wafw00f| Checked for and identified Web Application Firewall protection.
dnsrecon| Enumerated publicly available DNS records.
Zenmap| Provided a graphical interface for configuring and viewing Nmap scans.
Nmap| Performed host discovery across the internal lab subnet.
iproute2 ("ip addr show")| Helped me inspect the network interfaces and IP configuration of my Kali VM.
Windows Command Prompt ("ipconfig")| Used to inspect the Windows host's network configuration.

4. ACTIVITIES PERFORMED

4.1 W2-PM1: FOOTPRINTING AND RECONNAISSANCE USING KALI LINUX

The first module introduced me to the information-gathering stage of ethical hacking.

My task was to investigate networkwalks.com using six Kali Linux tools and document the information returned by each one.

I carried out the following activities.

4.1.1 WHOIS – Domain Registration Lookup

I started with WHOIS to retrieve the publicly available registration information associated with networkwalks.com.

Command executed:

whois networkwalks.com

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

The scan returned information about the web server, content management system, JavaScript libraries and plugins.

The technologies identified included:

- Web Server: Apache HTTP Server
- Server IP: 192.232.216.135
- WordPress: 7.0.4
- Bootstrap: 7.0.4
- jQuery: 3.7.1
- WordPress Download Manager: 3.3.58
- Contact Email: info@networkwalks.com

This was particularly interesting because it showed me how much information a website can reveal through technology fingerprinting.

I also learned why identifying software versions matters in cybersecurity. Security professionals can compare discovered versions with publicly documented security advisories to determine whether further investigation is necessary.

4.1.3 Nslookup – DNS Resolution

For the third task, I used nslookup to determine the IP address associated with the domain.

Command executed:

nslookup networkwalks.com

The query was resolved through Google Public DNS (8.8.8.8).

Result:

192.232.216.135

This confirmed the IPv4 address returned for networkwalks.com during my assessment.

This exercise helped me understand the relationship between domain names, IP addresses and DNS resolution.

4.1.4 Curl – HTTP Response Header Inspection

I then used curl to examine the HTTP response headers returned by the website.

Command executed:

curl -I https://networkwalks.com

The server returned:

HTTP/2 200 OK

The response also exposed several pieces of information, including:

- Apache server identification.
- HTTP response information.
- HttpOnly session cookie information associated with "__wpdm_client".
- Permissions-Policy header.
- A Link header referencing the WordPress REST API endpoint.

One of the interesting details was the reference to:

/wp-json/

This is associated with the WordPress REST API.

This task helped me understand that HTTP response headers can provide useful information about a website even without downloading and examining its entire page.

4.1.5 Wafw00f – Web Application Firewall Detection

For the fifth task, I used wafw00f to investigate whether a Web Application Firewall was protecting the target website.

Command executed:

wafw00f networkwalks.com

The result identified:

ModSecurity (SpiderLabs)

This indicated that the website was protected by a Web Application Firewall.

Before this exercise, I understood what a firewall was in general terms, but this practical task helped me appreciate the role of WAFs in protecting web applications by monitoring and filtering potentially harmful HTTP requests.

4.1.6 DNSRecon – DNS Enumeration

The final task in this module involved examining the DNS records associated with the domain.

Command executed:

dnsrecon -d networkwalks.com

DNSRecon returned information relating to the domain's DNS configuration, including name servers, mail exchange records, TXT records and other available service records.

The exercise introduced me to different DNS record types and their importance in understanding how a website's domain and associated services are configured.

It also helped me understand how DNS information can be useful during the reconnaissance stage of a security assessment.

Outcome of W2-PM1:

I completed the six reconnaissance exercises and gained practical experience using different Kali Linux tools to investigate publicly available information about a website.

---

4.2 W2-PM5: NETWORK SCANNING AND DISCOVERY WITH ZENMAP AND NMAP

The second module focused on identifying active devices within a local network.

Unlike the first module, which involved investigating a public domain, this exercise required me to examine my internal VirtualBox lab network.

My objectives were to:

- Identify my local IP address.
- Determine the network subnet.
- Discover active hosts.
- Count the discovered hosts.
- Identify their IPv4 addresses.
- Retrieve available MAC addresses.
- Generate and export a network topology diagram.

4.2.1 Initial Attempt and Troubleshooting

I initially attempted to carry out the network scan using Zenmap on my Windows host machine.

However, I encountered two major problems.

First, the scan returned zero active hosts in some attempts. Secondly, I could not obtain the MAC addresses of the discovered devices.

Rather than assuming that the network was empty or that the scanning tool was faulty, I decided to investigate the network configuration.

One important thing I had to understand was that MAC address discovery through ARP works within the local Layer 2 network segment. A scanner operating outside that segment may not be able to retrieve the hardware addresses of the target devices directly.

This made me reconsider where I was running the scan from.

4.2.2 Moving the Scanning Activity into Kali Linux

After the initial difficulties, I decided to carry out the scan directly inside my Kali Linux virtual machine.

My lab network was configured around the following subnet:

10.0.0.0/24

I also checked that DHCP was enabled on the VirtualBox network configuration.

To inspect the network interface inside Kali Linux, I executed:

ip addr show

This allowed me to examine the available interfaces and their assigned addresses.

I confirmed that my Kali Linux virtual machine had the following IPv4 address:

10.0.0.3

The address belonged to the:

10.0.0.0/24

subnet.

This confirmed that my Kali VM was operating within the lab network I intended to scan.

Running the scan from inside Kali Linux also gave me the opportunity to perform local network discovery with the appropriate privileges.

4.2.3 Performing the Network Scan

With the network configuration verified, I proceeded to perform a Ping Scan using Zenmap/Nmap.

Scan command:

nmap -sn 10.0.0.0/24

The "-sn" option instructs Nmap to perform host discovery without carrying out a port scan.

In simple terms, I was checking which devices were responding on the subnet rather than examining their open ports.

The scan was performed on 13 November 2026 at 11:23 (-0500).

Scan summary:

Scan Information| Result
Target Subnet| 10.0.0.0/24
Total IP Addresses Scanned| 256
Scan Duration| 3.07 seconds
Live Hosts Discovered| 3
Scanning Machine| Kali Linux VM
Scanning Machine IP| 10.0.0.3

4.2.4 Identifying the Live Hosts

The scan successfully identified three live hosts within the lab subnet.

The results were:

Host| IPv4 Address| MAC Address| Vendor / Description
Host 1| 10.0.0.1| 52:54:00:12:35:00| QEMU virtual NIC
Host 2| 10.0.0.2| 08:00:27:D9:21:01| Oracle VirtualBox virtual NIC
Host 3 (Local VM)| 10.0.0.3| Not displayed| Kali Linux Guest VM

The first host was identified as a QEMU virtual network interface, while the second was identified as an Oracle VirtualBox virtual network interface.

My Kali Linux virtual machine was the third live host and the machine from which I performed the scan.

An important observation was that Nmap did not display the MAC address of my own scanning machine in the results. I therefore documented it as unavailable rather than assuming or assigning an address.

4.2.5 Understanding the Results

This exercise helped me connect some networking concepts I had previously studied with what actually happens during a network scan.

For instance:

- An IP address helps identify a device within an IP network.
- A MAC address identifies a network interface at the Data Link Layer.
- ARP helps resolve IPv4 addresses to MAC addresses on a local network.
- A subnet defines the network range being examined.
- A Ping Scan helps identify active hosts without performing a port scan.

Seeing these details returned by an actual scan made the concepts much easier to understand.

4.2.6 Exporting the Network Topology to PDF

After completing the scan, I proceeded to generate the network topology diagram.

This was another part of the exercise that required some troubleshooting.

When I initially tried to save the topology, Zenmap populated the save location with an incorrect path.

The default location appeared as:

Desktop/.pdf

Since I was already working inside:

/home/kali/Desktop

the application attempted to access:

/home/kali/Desktop/Desktop

That directory did not exist, so the save operation returned a filesystem path error.

I had to go back and examine the save location rather than repeat the same action.

I resolved the issue by clearing the incorrect path, entering a clean filename and saving the file as:

topology.pdf

I saved the exported topology to my Kali Linux Desktop and subsequently transferred the PDF to my Windows host machine for documentation.

I also enabled the topology legend as instructed in the project guide.

Outcome of W2-PM5:

I successfully discovered three live hosts on my internal VirtualBox lab subnet, identified two MAC addresses and their associated virtual network interface vendors, and exported the network topology diagram as a PDF.

---

5. RISK ANALYSIS AND SECURITY OBSERVATIONS

The information gathered during both exercises provided an opportunity to identify areas that could be relevant during a security assessment.

The observations below are potential security considerations, not confirmed vulnerabilities.

No.| Observation| Evidence| Potential Security Implication| Assessed Risk
1| Website technology information is publicly identifiable.| WhatWeb identified Apache, WordPress, Bootstrap, jQuery and WP Download Manager versions.| Publicly identifiable software versions can help attackers research known vulnerabilities affecting those technologies.| Medium
2| The website's origin IP address is identifiable.| nslookup and WhatWeb returned 192.232.216.135.| The hosting infrastructure may be exposed to direct investigation, depending on the surrounding network protections.| Low
3| HTTP response headers expose server and API information.| Curl returned Apache identification and a WordPress REST API reference.| This information can assist further technology and endpoint enumeration.| Low
4| The Web Application Firewall can be identified.| Wafw00f detected ModSecurity (SpiderLabs).| Knowledge of the WAF technology can help an attacker understand the website's defensive setup.| Low
5| Public DNS information is available.| WHOIS and DNSRecon returned name server and other DNS information.| DNS information can help an attacker map hosting and email infrastructure and research possible weaknesses.| Medium
6| Multiple virtual hosts are visible on the internal lab subnet.| Nmap discovered three live hosts on 10.0.0.0/24.| Unauthorised devices on an insufficiently monitored internal network could introduce security risks.| Medium

Risk classification: Critical | Medium | Low.

The findings from this assessment represent information gathered during reconnaissance and host discovery. They do not establish that any of the identified systems has a confirmed exploitable vulnerability.

No intrusive exploitation, password attacks or denial-of-service activities were performed as part of these Week 2 exercises.

6. RECOMMENDATIONS

Based on the information gathered, I identified several areas that organisations can pay attention to when reviewing their security posture.

1. Review public technology information: Organisations should regularly review the information their websites expose about server software, CMS platforms and installed plugins.
2. Keep software updated: WordPress installations, plugins, themes and web server software should be maintained with appropriate security updates.
3. Review HTTP response headers: Website administrators should examine their HTTP response headers and ensure that unnecessary information is not exposed.
4. Maintain proper DNS security: DNS records, including SPF, DKIM and DMARC configurations, should be reviewed regularly to support domain and email security.
5. Maintain WAF protection: Organisations should keep their Web Application Firewalls updated and monitor them for suspicious activity.
6. Perform regular internal network discovery: Periodic authorised network scans can help organisations maintain an accurate record of devices connected to their networks.
7. Monitor virtualised network environments: When working with virtual machines, it is important to understand the network mode, subnet configuration and Layer 2 connectivity before performing network discovery.
8. Verify scan results: Security professionals should investigate unexpected results and confirm network configurations rather than immediately assuming that a scan has failed because of the tool itself.

7. CHALLENGES ENCOUNTERED AND LESSONS LEARNED

One of the most valuable parts of this week's practical work was troubleshooting.

Not everything worked as expected on the first attempt, and I had to spend time understanding why.

Here are some of the challenges I encountered and what I took away from them.

7.1 Network Scanning from Windows

My initial attempt to perform the scan from Zenmap on Windows did not give me the results I expected. Some scans returned zero live hosts, and MAC address information was not available.

What I learned: Before performing a network scan, I need to understand the network environment, the interface being used and whether the scanning machine is actually within the target subnet.

7.2 Understanding Layer 2 and MAC Address Discovery

I initially expected the scan to display the MAC addresses of all discovered hosts.

However, I learned that MAC address discovery through ARP depends on the scanner's position within the local network segment.

What I learned: IP-based communication and MAC address resolution operate at different networking layers. Understanding the distinction is important when troubleshooting network discovery.

7.3 Verifying the Kali Linux Network Configuration

Moving the scanning activity into my Kali Linux VM meant I had to verify its network configuration before proceeding.

I used:

ip addr show

This helped me confirm that the VM had the expected address of 10.0.0.3 on the 10.0.0.0/24 subnet.

What I learned: I should always verify the IP address, network interface and subnet before running a scan. Assuming that a virtual machine is connected to the correct network can lead to misleading results.

7.4 Zenmap Topology Export Error

I also encountered an error when exporting the network topology because of an incorrectly populated save path.

Rather than abandoning the export, I examined the path, corrected it and saved the file successfully.

What I learned: Even when working with graphical tools, understanding file paths and directory structures is important. Small configuration errors can prevent an otherwise successful task from being completed.

7.5 Overall Experience

This week's exercises reminded me that practical cybersecurity involves more than knowing commands and understanding what individual tools do.

Sometimes the real learning happens when something doesn't work as expected and you have to investigate the reason.

I also became more comfortable moving between Windows and Kali Linux, checking network configurations and interpreting the results returned by different security tools.

8. EVIDENCE AND DOCUMENTATION

The following evidence was collected during the practical exercises to support the activities and findings documented in this report.

Evidence| Module| Description
Evidence 1| W2-PM1| WHOIS output showing domain registration details, GoDaddy registrar and HostGator name servers.
Evidence 2| W2-PM1| WhatWeb output identifying Apache, WordPress 7.0.4 and WP Download Manager 3.3.58, among other technologies.
Evidence 3| W2-PM1| nslookup output confirming the IPv4 address 192.232.216.135.
Evidence 4| W2-PM1| Curl HTTP response headers showing HTTP/2 200 OK and the WordPress REST API reference.
Evidence 5| W2-PM1| Wafw00f output identifying ModSecurity (SpiderLabs).
Evidence 6| W2-PM5| Zenmap/Nmap Ping Scan showing three live hosts on 10.0.0.0/24, including the available MAC addresses.
Evidence 7| W2-PM5| Exported network topology diagram (topology.pdf) with the legend enabled.

The evidence files accompany this report to provide a record of the practical activities performed.

9. CONCLUSION

Completing Week 2 of my Cybersecurity Internship at Networkwalks gave me the opportunity to apply some of the concepts I had been learning to actual cybersecurity exercises.

Through W2-PM1, I worked with six Kali Linux tools to investigate the publicly available information associated with networkwalks.com. I was able to retrieve domain registration details, identify website technologies, resolve its IP address, inspect HTTP response headers, detect its Web Application Firewall and enumerate DNS information.

W2-PM5 took me further into practical networking. I initially encountered difficulties with network discovery and MAC address identification while attempting to scan from Windows. After investigating the issue, I moved the scanning activity into my Kali Linux virtual machine, verified its network configuration and successfully performed a Ping Scan on my internal VirtualBox subnet.

The scan identified three live hosts:

- 10.0.0.1
- 10.0.0.2
- 10.0.0.3

I also identified two MAC addresses, examined their virtual network interface vendors and successfully exported the network topology diagram after resolving a file path issue.

Beyond completing the assigned tasks, this week's experience helped me better understand how reconnaissance, DNS resolution, host discovery, IP addressing, ARP and network topology relate to one another.

Most importantly, I learned not to stop when a tool returns an unexpected result. Understanding the environment, checking configurations and troubleshooting systematically are all part of working in cybersecurity.

I consider this another important step in developing my practical cybersecurity skills.

---

AUTHOR

Precious Doowuese Dagba
Cybersecurity Intern | Networkwalks

PROGRAMME: Cybersecurity Internship Program – Networkwalks
PROJECT: Week 2 – Footprinting & Network Scanning
MODULES: W2-PM1 | W2-PM5
DATE: 13 November 2026

All activities documented in this report were conducted within the scope of the authorised educational exercises.