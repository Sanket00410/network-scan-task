# Network Scanning Task

## Overview
This repository contains the results and analysis of a **local network scanning task** performed using **Nmap** and optionally **Wireshark**.  
The goal of this task was to discover open ports on devices in the local network, analyze potential risks, and suggest security hardening measures.

---

## Tools Used
- **Nmap** – Free network scanning tool: [https://nmap.org](https://nmap.org)
- **Wireshark (optional)** – Packet analysis tool: [https://www.wireshark.org](https://www.wireshark.org)

---

## Task Execution

### Step 1: Identify Local Network
- Local IP range: `192.168.*.0/24`
- Found live hosts using a ping sweep:  
  ```bash
  nmap -sn 192.168.*.0/24
Step 2: TCP SYN Scan

Performed SYN scan to discover open ports:

sudo nmap -sS 192.168.*.0/24 -oA nmap_scan

Step 3: Service Detection

Detected services and versions (optional):

sudo nmap -sS -sV 192.168.*.*

Step 4: Save Results

CSV summary: nmap_scan_summary.csv

Detailed HTML report: nmap_scan_detailed_report.html

Full report with interpretation & recommendations: nmap_scan_full_report.html

Scan Results Summary
Host	IP	Open Ports	Risk Level	Risk Description
Windows Host Adapter	192.168.*.*	135/tcp (MSRPC), 139/tcp (NetBIOS)	Medium	Exposes Windows RPC and NetBIOS services. Potential for lateral movement or SMB relay attacks.
VirtualBox VM	192.168.*.*	None (All filtered)	Low	Firewall blocks all ports. Minimal exposure.
Ubuntu VM	192.168.*.*	None (All closed)	Low	Host alive but no services listening. Minimal exposure.

(Refer to nmap_scan_detailed_report.html for full interpretation.)
