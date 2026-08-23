# PENETRATION TESTING REPORT

## FOOTPRINTING & NETWORK SCANNING PHASES
─────────────────────────────────────────────────────────────────────────────────

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red)
![Kali](https://img.shields.io/badge/Kali_Linux-v2026.1-purple)
![Skill](https://img.shields.io/badge/Skill-Linux-red)
![Network](https://img.shields.io/badge/Network-192.168.x.x/24-black)
![Skill](https://img.shields.io/badge/Penetration_Testing-Skill-red)
![Skill](https://img.shields.io/badge/Skill-Virtualization-red)
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
| IP Route | Local IP address, interface, route and gateway identification. |

---


