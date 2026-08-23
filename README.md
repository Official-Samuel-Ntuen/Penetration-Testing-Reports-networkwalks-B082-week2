# <h1 align="center">PENETRATION TESTING REPORT</h1>

## <h1 align="center">FOOTPRINTING & NETWORK SCANNING PHASES</h1>
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
