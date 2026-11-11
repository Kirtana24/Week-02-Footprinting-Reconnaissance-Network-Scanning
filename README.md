# Week 02 – Footprinting, Reconnaissance & Network Scanning

**Cybersecurity Internship | Networkwalks**

## Objectives

The objectives of Week 2 were:

- To understand the basics of footprinting and reconnaissance.
- To gather publicly available information about a target domain.
- To identify website technologies and DNS information using Kali Linux tools.
- To detect the presence of a Web Application Firewall (WAF).
- To perform network discovery using Zenmap.
- To identify active hosts and understand network topology.

## Lab Environment

- **Operating System:** Kali Linux
- **Network Scanning Tool:** Zenmap / Nmap 7.99
- **Footprinting Tools:** WHOIS, WhatWeb, Nslookup, cURL, Wafw00f and DNSRecon
- **Target Domain:** networkwalks.com
- **Local Network Interface:** eth0
- **Local IP Address:** 10.0.0.3/24
- **Network Subnet:** 10.0.0.0/24

## Authorization and Scope

The footprinting activity involved gathering publicly available information from the target domain, networkwalks.com. The network scanning activity was restricted to my local VirtualBox lab network (10.0.0.0/24).

No exploitation, password attacks or disruptive testing were performed.

## Practical 1 – Footprinting and Reconnaissance (W2-PM1)

The objective of this practical was to collect information about the target domain using six different Kali Linux tools.

### 1. WHOIS – Domain Information Gathering

WHOIS was used to collect domain registration details.

**Command Used:**
```bash
whois -h whois.verisign-grs.com networkwalks.com
```

**Observations:**
- Registrar: GoDaddy.com, LLC.
- Creation Date: 06 November 2019.
- Expiry Date: 06 November 2027.
- Nameservers: NS6135.HOSTGATOR.COM and NS6136.HOSTGATOR.COM.
- DNSSEC: Unsigned.

### 2. WhatWeb – Website Technology Identification

WhatWeb was used to identify the technologies and software used by the target website.

**Command Used:**
```bash
whatweb https://networkwalks.com
```

**Observations:**
- HTTP Status: 200 OK.
- Web Server: Apache.
- CMS: WordPress.
- Detected technologies included Bootstrap, jQuery and WordPress Download Manager.
- Website Title: Networkwalks Academy.

### 3. Nslookup – DNS Lookup

Nslookup was used to resolve the domain name and identify its associated IP addresses.

**Command Used:**
```bash
nslookup networkwalks.com
```

**Observations:**
- DNS Server: 172.20.10.1.
- IPv4 Address: 192.232.216.135.
- IPv6-format NAT64 Address: 64:ff9b::c0e8:d887.

### 4. cURL – HTTP Response Analysis

cURL was used to inspect the HTTP response headers returned by the website.

**Command Used:**
```bash
curl -I https://networkwalks.com
```

**Observations:**
- HTTP Response: 200 OK.
- Server: Apache.
- Content-Type: text/html.
- WordPress REST API endpoint information was visible.
- Security-related response headers were observed.

### 5. Wafw00f – Web Application Firewall Detection

Wafw00f was used to identify whether a Web Application Firewall was present.

**Command Used:**
```bash
wafw00f https://networkwalks.com
```

**Observations:**
- Detected WAF: ModSecurity (SpiderLabs).
- The detection was completed using two HTTP requests.

### 6. DNSRecon – DNS Enumeration

DNSRecon was used to gather additional DNS records associated with the target domain.

**Command Used:**
```bash
dnsrecon -d networkwalks.com
```

**Observations:**
- Total DNS Records Found: 16.
- SOA, NS, MX, A, AAAA, TXT and SRV records were identified.
- Mail server: mail.networkwalks.com.
- SPF and Google site verification TXT records were identified.
- Nameserver information and DNS-related details were collected.

## Evidence – Footprinting and Reconnaissance

1. WHOIS - Domain Information

<img width="1917" height="1020" alt="PM1_01_WHOIS 1" src="https://github.com/user-attachments/assets/80b69e4e-e9ab-4ff8-80d9-e8ecd485de7a" />
<img width="1917" height="1016" alt="PM1_01_WHOIS 2" src="https://github.com/user-attachments/assets/178e46e8-991f-4add-a519-1256ebf48b04" />

2. WhatWeb - Technology Identification

<img width="1907" height="152" alt="PM1_02_WhatWeb" src="https://github.com/user-attachments/assets/7a22e1e0-8646-4699-aaba-dba62844b347" />

3. Nslookup - DNS Lookup

<img width="1897" height="255" alt="PM1_03_NSLookup" src="https://github.com/user-attachments/assets/b950cfe1-989c-43af-bdc4-1fb28afe22dc" />

4. cURL - HTTP Response

<img width="1892" height="231" alt="PM1_04_CURL" src="https://github.com/user-attachments/assets/3f492585-6693-4bf5-a702-6c432e7ce7ca" />

5. Wafw00f - WAF Detection

<img width="675" height="262" alt="PM1_05_WAFW00F" src="https://github.com/user-attachments/assets/b5cb3377-cc38-4b96-850c-30247f297275" />

6. DNSRecon - DNS Enumeration

<img width="1325" height="627" alt="PM1_06_DNSRecon" src="https://github.com/user-attachments/assets/788e37bc-c43e-42ca-a40f-00f1d6f394e3" />

## Practical 2 – Network Scanning Using Zenmap (W2-PM5)

### Objective

The objective of this practical was to discover active hosts in a local network and understand the network topology using Zenmap.

### Tools Used

- Kali Linux
- Zenmap
- Nmap 7.99

### Network Details

- Network Interface: eth0
- IP Address: 10.0.0.3/24
- Network Range: 10.0.0.0/24

### Command Used

```bash
ip -br addr
```

The command was used to identify the active network interface and IP address.

A Ping Scan was then performed in Zenmap on the subnet 10.0.0.0/24.

### Active Hosts Discovered

The scan identified three active hosts:

| IP Address | MAC Address / Identification |
|---|---|
| 10.0.0.1 | 52:55:0A:00:00:01 – Unknown vendor |
| 10.0.0.2 | 08:00:27:AE:38:62 – Oracle VirtualBox virtual NIC |
| 10.0.0.3 | Kali Linux machine used for scanning |

**Scan Details:**
- Scan Type: Ping Scan.
- IP Addresses Scanned: 256.
- Active Hosts Found: 3.
- Scan Duration: Approximately 3.08 seconds.

### Network Topology

The Topology section in Zenmap displayed the discovered hosts through a graphical network diagram consisting of circles and connecting lines.

**Note:** The activity involved host discovery only. No port or service scanning was performed.

## Evidence – Network Scanning

1. Nmap / Zenmap Host Discovery

<img width="1917" height="1017" alt="PM5_01_Zenmap_PingScan" src="https://github.com/user-attachments/assets/d9f27677-6cf9-4d4c-a10b-8ff17b16a37d" />

2.Zenmap Network Topology

<img width="1917" height="1020" alt="PM5_02_Zenmap_Topology" src="https://github.com/user-attachments/assets/a1113f9a-88e8-4a4a-8d3d-6c19eae027d9" />

## Consolidated Findings

No.	Practical	Tool Used	Key Findings
1	PM1 – Footprinting	WHOIS	Identified registrar, domain creation and expiry dates, and nameservers.
2	PM1 – Footprinting	WhatWeb	Identified Apache, WordPress, Bootstrap, jQuery and other website technologies.
3	PM1 – Footprinting	Nslookup	Resolved networkwalks.com to IPv4 address 192.232.216.135.
4	PM1 – Footprinting	cURL	Retrieved HTTP 200 response and inspected server response headers.
5	PM1 – Footprinting	Wafw00f	Detected ModSecurity (SpiderLabs) Web Application Firewall.
6	PM1 – Footprinting	DNSRecon	Identified 16 DNS records, including SOA, NS, MX, TXT and SRV records.
7	PM5 – Network Scanning	Zenmap	Discovered three active hosts in the 10.0.0.0/24 subnet.
8	PM5 – Network Scanning	Zenmap Topology	Generated a graphical representation of the discovered network hosts.

## Risk Analysis

#	Risk / Finding	Evidence / Observation	Potential Impact	Risk Level
1	Web technology information exposed	WhatWeb identified WordPress 7.1.4 and WordPress Download Manager 3.3.76.	Attackers may use exposed technology and version information to identify software requiring further security review.	🟠 Medium
2	Server IP address identifiable	Nslookup resolved the domain to 192.232.216.135.	Provides information about the network location of the web service.	🟡 Low
3	HTTP technical information exposed	cURL returned HTTP response headers and exposed the /wp-json/ endpoint.	May assist technology fingerprinting and further enumeration.	🟡 Low
4	WAF technology identifiable	Wafw00f identified ModSecurity (SpiderLabs) WAF.	Reveals information about the web application's security architecture.	🟡 Low
5	DNS infrastructure information exposed	DNSRecon identified 16 DNS records, including SOA, NS, MX, TXT and SRV records.	DNS information can help build a broader infrastructure profile.	🟠 Medium
6	Multiple live hosts visible on local network	Zenmap identified three live hosts: 10.0.0.1, 10.0.0.2 and 10.0.0.3.	Unknown or unauthorised devices may potentially be present on a network.

## Security Recommendations

1. Regularly review publicly exposed website technology information.
2. Keep WordPress, plugins and other web technologies updated.
3. Review HTTP response headers to minimise unnecessary information disclosure.
4. Regularly review DNS records and remove unnecessary entries.
5. Properly configure and monitor the Web Application Firewall.
6. Perform periodic network discovery within authorised networks.
7. Investigate unknown devices connected to the network.
8. Maintain updated network documentation and topology diagrams.
9. Perform security testing only within an authorised scope.

## Learning Outcomes

Through these practical activities, I learned:

- How to collect domain registration information using WHOIS.
- How to identify website technologies using WhatWeb.
- How to resolve domain names using Nslookup.
- How to inspect HTTP response headers using cURL.
- How to identify Web Application Firewalls using Wafw00f.
- How to enumerate DNS records using DNSRecon.
- How to perform network discovery using Zenmap.
- How to identify active hosts and interpret network topology diagrams.

## Conclusion

During Week 2 of my Cybersecurity and Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance and network scanning.

I used six Kali Linux tools to gather information about networkwalks.com and performed a Ping Scan using Zenmap to identify active hosts in my local VirtualBox network.

These activities improved my understanding of information gathering, website technology identification, DNS enumeration and network discovery. I also learned the importance of analysing findings, documenting observations and following an authorised testing scope.

## Project Report 

The detailed Week 02 practical report, including methodology, tools used, observations, scan results, and recommendations, is available below.

## Author

**Name:** Kirtana Minoy
Cybersecurity Intern – Networkwalks Internship: Networkwalks
**Program/Batch:** B084D-Networkwalks
**Domain** Cybersecurity
**Week:** 02
**Modules:** W2-PM1 and W2-PM5
