# PENETRATION TESTING REPORT</p>
## FOOTPRINTING & NETWORK SCANNING PHASES
─────────────────────────────────────────────────────────────────────────────────

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red)
![Kali](https://img.shields.io/badge/Kali_Linux-v2026.1-purple)
![Skill](https://img.shields.io/badge/Skill-Linux-red)
![Network](https://img.shields.io/badge/Network-192.168.x.x/24-black)
![Skill](https://img.shields.io/badge/Penetration_Testing-Skill-red)
![Skill](https://img.shields.io/badge/Skill-Footprinting--&--Network--Scanning-red)
![GitHub](https://img.shields.io/badge/GitHub-Official--Samuel--Ntuen-black?logo=github)
![NetworkWalks](https://img.shields.io/badge/NetworkWalks-orange)
![Ethical](https://img.shields.io/badge/Ethical_Hacking-darkgreen)
![Waqas](https://img.shields.io/badge/-Samuel_M._Ntuen-red)
---

| Field | Details |
|---|---|      
| Pentester | Samuel Ntuen |
| Program / Batch | B082-Networkwalks |
| Date | 23 August 2026 |
| Modules Completed | • W2-PM1 (Multiple Kali Reconnaissance Tools)<br> • W2-PM2 (Google Hacking Database - GHDB)<br> • W2-PM3 (Maltego Visual OSINT)<br> • W2-PM4 (theHarvester Passive Discovery)<br> • W2-PM5 (Zenmap & Nmap Subnet Scanning)|
| Client / Target | 1. Networkwalks (networkwalks.com — secured written permission already)<br> 2. My own local LAN Network (192.168.xx.x/24)|
| Permission | Yes |
| Phases Covered | • Phase 1: Reconnaissance & Footprinting<br> • Phase 2: Scanning & Network Discovery<br> • Phase 3–5: In Progress |

---
## 📌 Liability Disclaimer
I have performed these activities only on systems and devices where I had secured written permission, or devices and systems that I own myself. All these materials are for education and research purposes only. Do not use anything from here to break the law. The instructor, the authors, and NetworkWalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job, and a permanent record. In most countries, unauthorised access is a crime even when nothing is damaged.

---

## 📌 Introduction

This report covers footprinting the networkwalks.com domain using six Kali Linux tools (W2-PM1), performing Google Dorking with GHDB (W2-PM2), visual OSINT mapping with Maltego (W2-PM3), passive harvesting with theHarvester (W2-PM4), and scanning my own local network with Zenmap (W2-PM5).

Together, these modules show how an attacker moves from gathering public information to mapping live hosts on a network. This is the Week 2 part of my ongoing cybersecurity internship program at NetworkWalks Academy under the mentorship of Waqas Karim CCIE.

All commands were running in Kali Linux 2026.1. Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view.

---

## 📌 Tools Used

| Tool | Purpose |
|---|---|
| WHOIS | Domain registration and ownership information gathering. |
| WhatWeb | Web technology and server fingerprinting (CMS, plugins, IP). |
| Nslookup | DNS resolution and IP address discovery. |
| Curl | HTTP header and server information gathering. |
| Wafw00f | Web Application Firewall detection. |
| DNSRecon | Enumerate all DNS records (NS, MX, SPF, TXT, SRV). |
| Google Hacking (GHDB) | Find exposed cameras and downloadable academic PDF documents using search dorks. |
| Maltego | Visual OSINT and relationship mapping. |
| theHarvester | Passive Reconnaissance and OSINT collection |
| Zenmap | Network discovery and port scanning. |
| Kali Linux | Operating systems used for reconnaissance and scanning activities. |
| Kali Linux CMD (`IP Route`) | Local IP address, interface, route and gateway identification. |

---

## 📌 Activities Performed

### a. Footprinting & Reconnaissance (W2-PM1)

I performed reconnaissance against the `networkwalks.com` domain using six Kali Linux tools: **WHOIS**, **WhatWeb**, **Nslookup**, **Curl**, **Wafw00f**, and **DNSRecon**.

- **WHOIS**: Queried domain registration details, revealing GoDaddy as registrar, active dates (2019–2027), HostGator nameservers (`ns6135.hostgator.com`, `ns6136.hostgator.com`), and WHOIS privacy protection.
- **WhatWeb**: Identified WordPress 7.0.4, WP Download Manager 3.3.58, Apache web server, jQuery 3.7.1, Bootstrap 7.0.4, and IP address `192.232.216.135`.
- **Nslookup**: Resolved `networkwalks.com` to its direct host IP `192.232.216.135`.
- **Curl -I**: Retrieved HTTP/2 200 response headers, exposing Apache server, caching headers (`x-nginx-cache: WordPress`), and the WordPress REST API endpoint `/wp-json/`.
- **Wafw00f**: Detected that the website is protected by **ModSecurity (SpiderLabs) WAF**. The captured output also showed several HTTP response signatures, including:
• 404
• 405
• 403
• 502
• 500

These responses were observed during WAF fingerprinting and do not by themselves indicate vulnerabilities.
- **DNSRecon**: Enumerated DNS records including NS, SOA, MX (`mail.networkwalks.com`), SPF records, cPanel autodiscover SRV records, and exposed BIND version `9.16.23-RH`.

---

### b. Search Engine Footprinting & GHDB (W2-PM2)

I used Google search operators (`intitle:`, `inurl:`, `site:`, `filetype:`) to locate publicly accessible camera feeds and downloadable academic mathematics resources *(IP endpoints partially sanitized)*:

#### 10x Live Vulnerable / Exposed Security Cameras (Sanitized Endpoints)
| No. | Target Link (Sanitized) | Relevant Dork | Access Status |
| :-: | :--- | :--- | :--- |
| 1 | `http://122.116.41.xxx:8080/` | `intitle:"webcamXP" inurl:8080` | Open webcamXP live stream |
| 2 | `https://www.lmc.edu/webcam.htm` | `intitle:"Webcam" inurl:WebCam.htm` | Public campus webcam |
| 3 | `http://198.41.49.xxx:81/main.htm` | `intitle:"Device(IP CAMERA)" "language" -com\|net` | Direct IP camera stream |
| 4 | `http://86.122.80.xxx/Pages/login.htm` | `intitle:"NoVus IP camera" -com` | NoVus camera login interface |
| 5 | `https://www.skylinewebcams.com/en/webcam/...` | `inurl:webcam site:skylinewebcams.com inurl:roma` | Public live broadcast feed |
| 6 | `https://www.skylinewebcams.com/en/webcam/...` | `inurl:webcam site:skylinewebcams.com inurl:roma` | Public live broadcast feed |
| 7 | `http://109.233.191.xxx:8080/multi.html` | `intitle:"webcamXP" inurl:8080` | Multi-channel webcamXP stream |
| 8 | `http://72.199.200.xxx:8080/` | `intitle:"Index of" "DCIM/camera"` | Open directory with camera files |
| 9 | `http://139.64.168.xxx:8080/` | `intitle:"Index of" "DCIM/camera"` | Open directory camera media storage |
| 10 | `http://75.149.26.xxx:1024/` | `intitle:"webcamXP" inurl:8080` | webcamXP stream on port 1024 |

#### 10x Downloadable Mathematics Ebooks / Lecture Notes
| No. | Link | Relevant Dork | Institution / Topic |
| :-: | :--- | :--- | :--- |
| 1 | `https://www.skylineuniversity.ac.ae/pdf/math/` | `intitle:index.of "parent directory" mathematics pdf` | Skyline University (Math Directory) |
| 2 | `https://www.math.k-state.edu/~gerald/math220d/lec1.pdf` | `site:.edu filetype:pdf "calculus" "lecture notes"` | Kansas State University (Calculus) |
| 3 | `https://empslocal.ex.ac.uk/people/staff/mrwatkin/zeta/knauf1.pdf` | `site:.ac.uk ext:pdf "number theory" "introduction"` | University of Exeter (Number Theory) |
| 4 | `https://math.nd.edu/assets/150763/60610_basic_discrete_mathematics.pdf` | `site:math.*.edu filetype:pdf "discrete mathematics"` | Notre Dame (Discrete Mathematics) |
| 5 | `https://www.maths.usyd.edu.au/u/UG/HM/coordinator/applied2025.pdf` | `site:.edu.au ext:pdf "applied mathematics"` | University of Sydney (Applied Math) |
| 6 | `https://cas.minesparis.psl.eu/~rouchon/publications/PR1993/INDEXLIN.pdf` | `intitle:"index of" "linear algebra" pdf` | Mines Paris (Linear Algebra) |
| 7 | `https://people.tamu.edu/~e-straube/Math618/syllabusFall2024.pdf` | `inurl:syllabus filetype:pdf "complex variables"` | Texas A&M (Complex Variables) |
| 8 | `https://ramanujan.math.trinity.edu/wtrench/texts/TRENCH_REAL_ANALYSIS.PDF` | `ext:pdf inurl:course "real analysis"` | Trinity University (Real Analysis) |
| 9 | `https://math.njit.edu/sites/math/files/Math_279-001-003-F20.pdf` | `inurl:downloads filetype:pdf "statistics and probability"` | NJIT (Statistics & Probability) |
| 10 | `https://mrcet.com/downloads/digital_notes/ME/II%20year/MATERIAL%20SCIENCE.pdf` | `inurl:materials filetype:pdf "geometry"` | MRCET Digital Notes |

---

### c. Maltego Visual OSINT (W2-PM3)
Using Maltego Graph 4.12.1, I performed visual entity mapping and relationship analysis:
- Configured Maltego Data Hub transforms.
- Ran email transforms against `networkwalks.com` to confirm domain contacts (`info@networkwalks.com`).

---

### d. theHarvester Footprinting (W2-PM4)
Using theHarvester 4.10.1, I conducted passive subdomain and email discovery.
Ran `theHarvester -d networkwalks.com -l 1000 -b all`.
Discovering:
- 3 ASNs identified (AS13335 / Cloudflare, AS31898, AS46606)
- 2 public IPs: 172.67.xxx.xxx, 192.232.xxx.xxx (masked — Cloudflare / hosting provider range, full addresses in report)
- 1 public contact email: info@networkwalks.com
- 23 subdomain/host records (cpanel, webmail, autodiscover, mail, ftp, etc.)

---

### e. Network Scanning with Zenmap (W2-PM5)
For the internal scanning activity, I performed host discovery and port enumeration on my local LAN (`192.168.x.x/24`).

* Ran `ip route` on Kali Linux to identify my local IP address `192.168.x.xxx/24`, subnet mask `/24` (`255.255.xxx.0`), and default gateway `192.168.0.1` through the `wlan0` interface.
* Executed `nmap -T4 -F 192.168.0.xxx/24` in Zenmap.
* Discovered 3 active hosts on the network:

  * `192.168.0.1` (Gateway/Router): Ports **53/tcp (DNS)** and **80/tcp (HTTP)** open (MAC address sanitized).
  * `192.168.x.xxx`: **77/tcp filtered**; service was not identified (MAC address sanitized).
  * `192.168.x.xxx` (Kali Linux Workstation): Host is up, but all 100 scanned TCP ports were **filtered** with no response.

---
## 📌  Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks:

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
| :-: | :--- | :--- | :--- | :-: |
| 1 | **Web technology information disclosed** | WhatWeb identified WordPress 7.0.4 and WP Download Manager 3.3.58 | Can assist technology fingerprinting and vulnerability research. | 🟡 **Medium** |
| 2 | **DNS information exposed** | DNSRecon identified DNS, MX, SPF records and BIND version `9.16.23-RH` | Disclosing daemon versions assists in building targeted infrastructure profiles. | 🟡 **Medium** |
| 3 | **Multiple live hosts visible on local network** | Zenmap identified 3 live hosts, ports 53/tcp and 80/tcp on `192.168.x.x/24` | Provides visibility of devices on the local network. | 🟡 **Medium** |
| 4 | **Server IP address identifiable** | Nslookup resolved domain to `192.232.216.135` | Provides the direct network location of the web service. | 🟢 **Low** |
| 5 | **HTTP technical information exposed** | Curl returned response headers and exposed `/wp-json/` | Assists in technology fingerprinting and REST API route enumeration. | 🟢 **Low** |
| 6 | **WAF technology identifiable** | Wafw00f identified ModSecurity (SpiderLabs) | Reveals perimeter security architecture to an attacker. | 🟢 **Low** |
| 7 | **Email address harvested** | WhatWeb + theHarvester — info@networkwalks.com | Can be used for phishing or social engineering attacks. | 🟢 **Low** |

**Risk Level Key**: 🔴 Critical | 🟡 Medium | 🟢 Low

The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities. The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these modules.

Therefore, the presence of information such as a software version, IP address, or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

---

## 📌 Recommendations

Based on the observations from these activities, I recommend the following security improvements:

1. **Review publicly exposed technology information**: Regularly check what web technologies, CMS versions, and plugins are publicly visible.
2. **Keep software updated**: Ensure WordPress core, plugins, and web servers are routinely patched.
3. **Review HTTP headers**: Suppress unnecessary server banners and add security headers (`HSTS`, `CSP`, `X-Frame-Options`).
4. **Review DNS records regularly**: Periodically audit DNS and suppress BIND version banner leakage.
5. **Properly configure and monitor the WAF**: Keep ModSecurity enabled and tuned with updated rule sets.
6. **Perform regular internal network discovery**: Periodically scan internal subnets to identify unauthorized or rogue devices.
7. **Secure internal SMB and NetBIOS**: Restrict inbound access to ports 135, 139, and 445 on local workstations.
8. **Disable UPnP on gateway devices**: Turn off UPnP on routers to prevent automated port forwarding.
9. **Maintain network documentation**: Keep network topology diagrams and IP address assignments updated.
10. **Perform security testing with authorization**: Always ensure scanning and OSINT testing are conducted within an authorized scope.

---

## 📌 Conclusion

The Week 2 internship activities provided practical experience in reconnaissance, OSINT, web technology fingerprinting, DNS enumeration, WAF detection, and network scanning.

The footprinting phase demonstrated how multiple reconnaissance tools can be combined to build an understanding of a target's infrastructure.

WHOIS provided domain registration information, WhatWeb identified web technologies, Nslookup identified the target IP, Curl exposed HTTP response information, Wafw00f detected ModSecurity, and DNSRecon identified DNS records.

Maltego provided a visual representation of relationships associated with the target, while theHarvester successfully collected ASNs, IP addresses, an email address, URLs, and 21 host entries from the selected sources.

The Zenmap exercise provided practical experience in identifying live hosts and open or filtered ports within a local /24 network.

Overall, the exercises demonstrated that reconnaissance and network scanning are important stages of a penetration testing methodology because they help security professionals understand the target environment before performing deeper security assessments.

---

## 📌 Evidences Collected

### a. Footprinting & Reconnaissance Evidence (W2-PM1)

#### WHOIS Query Output (`whois networkwalks.com`)
*Shows domain registration, GoDaddy registrar, and HostGator nameservers.*
![WHOIS Query Result](pm1/task1_whois.png)
