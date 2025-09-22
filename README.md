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

**Wireshark Analysis**
Capture file: capture.pcapng
Observed interesting packets using filters:
ip.addr == 192.168.*.*
tcp.port == 135
Example packets table included in wireshark_analysis_report.html

**Recommendations**:
Monitor unusual SYN packets to sensitive ports
Ensure firewall rules block unnecessary connections
Disable legacy services (SMB v1, NetBIOS)
Segment VM networks from main LAN

**Security Hardening Recommendations**
Disable unused services (e.g., SMB/NetBIOS if not needed).
Block high-risk ports via firewall (e.g., 135, 139).
Restrict access to sensitive services to internal or trusted IPs only.
Keep systems updated and patched.
Monitor network for unusual traffic patterns.

**Files in this Repository**
nmap_scan_summary.csv – CSV summary of Nmap scan results.
nmap_scan_full_report.html – Full report with interpretation and recommendations.
wireshark_analysis_report.html – Optional Wireshark packet analysis report.
Capture.pcapng – Optional raw Wireshark capture file.

**Note**
All tools used are free and open-source.
Task performed safely on local VM network (no external scanning).
Self-research and debugging applied to resolve issues encountered during scanning.
