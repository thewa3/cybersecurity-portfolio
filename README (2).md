# 🗺️ Nmap Network Reconnaissance & Port Scanning

## Overview
This project documents a full network reconnaissance exercise performed on my virtual home lab using Nmap (Network Mapper). Starting from zero knowledge of the network, I systematically discovered live hosts, identified open ports, enumerated running services, and exported results — replicating the exact methodology used by real penetration testers during the reconnaissance phase of an engagement.

---

## Target Environment

| Detail | Value |
|--------|-------|
| **Attacker Machine** | Kali Linux (IP: 192.168.1.10) |
| **Target Network** | 192.168.1.0/24 |
| **Target Host** | 192.168.1.20 (VMware machine) |
| **Tool Used** | Nmap 7.95 |
| **Date** | June 14, 2026 |

---

## Reconnaissance Methodology

### Step 1 — Network Configuration Check
```bash
ifconfig
netstat -na
```
Before scanning, I verified my own machine's network configuration using `ifconfig` to confirm my IP address (192.168.1.10) and used `netstat -na` to view all active connections and listening ports on the attacker machine.

---

### Step 2 — Host Discovery (Ping Sweep)
```bash
nmap -sn 192.168.1.0/24
```
Scanned the entire /28 subnet to discover which hosts were alive. Results:
- **192.168.1.1** — Host up (0.0058s latency)
- **192.168.1.10** — Host up (0.00034s latency) — Intel Corporate NIC
- **192.168.1.20** — Host up (0.00063s latency) — VMware NIC
- **192.168.1.30** — Host up

**Total: 4 hosts discovered out of 16 IP addresses**

---

### Step 3 — Port Scan Without Ping (Pn flag)
```bash
nmap -Pn 192.168.1.0/24
```
Scanned all hosts while skipping the ping check — useful when hosts block ICMP. Discovered open ports across multiple machines including FTP (21), SSH (22), Telnet (23), SMTP (25), HTTP (80), and more.

---

### Step 4 — Stealth SYN Scan
```bash
nmap -sS 192.168.1.20
```
Performed a stealthy half-open SYN scan against the target. This scan is harder to detect because it never completes the TCP handshake. Discovered 20+ open ports including:

| Port | Service |
|------|---------|
| 21/tcp | FTP |
| 22/tcp | SSH |
| 23/tcp | Telnet |
| 25/tcp | SMTP |
| 80/tcp | HTTP |
| 445/tcp | Microsoft-DS |
| 3306/tcp | MySQL |
| 5432/tcp | PostgreSQL |
| 5900/tcp | VNC |
| 6000/tcp | X11 |

---

### Step 5 — Full TCP Connect Scan
```bash
nmap -sT 192.168.1.20
```
Performed a full TCP connect scan — completes the full three-way handshake. Confirmed same open ports as the SYN scan. Used to verify results.

---

### Step 6 — Fast Scan
```bash
nmap -F 192.168.1.20
```
Quick scan of the most common 100 ports. Completed in 0.49 seconds. Useful for rapid initial assessment.

---

### Step 7 — UDP Scan
```bash
nmap -sU -p53,137 192.168.1.20
```
Scanned specific UDP ports. Discovered:
- **53/udp** — DNS (domain) open
- **137/udp** — NetBIOS-ns open

---

### Step 8 — Aggressive Scan (Service & Version Detection)
```bash
nmap -A 192.168.1.20
```
Full aggressive scan revealing detailed service versions and configurations:
- **FTP (21)** — vsFTPd 2.3.4 — Anonymous login allowed (FTP code 230)
- **MySQL (3306)** — Version 5.0.51a-3ubuntu5, Protocol 10
- **PostgreSQL (5432)** — Version 8.3.0 – 8.3.7
- **Samba (139/445)** — smbd 3.X-4.X, Workgroup: WORKGROUP
- **VNC (5900)** — Protocol version 3.3
- **Metasploitable root shell (1524)** — bindshell detected

---

### Step 9 — Output to File
```bash
nmap -sS 192.168.1.20 -oS kiddie.txt
```
Exported scan results to a text file (`kiddie.txt`) for documentation and reporting — a standard practice in real penetration testing engagements.

---

## Key Findings

| Vulnerability | Risk Level | Detail |
|--------------|-----------|--------|
| Anonymous FTP login | 🔴 High | vsFTPd allows login without credentials |
| Telnet open | 🔴 High | Unencrypted remote access protocol |
| Metasploitable shell | 🔴 Critical | Port 1524 bindshell — direct root access |
| MySQL exposed | 🟠 Medium | Database port open to network |
| Old SSL certificate | 🟠 Medium | PostgreSQL cert expired since 2010 |

---

## Skills Demonstrated

- Network host discovery and subnet scanning
- Multiple Nmap scan types (SYN, TCP, UDP, Aggressive, Fast)
- Service and version enumeration
- Vulnerability identification from scan results
- Network interface configuration (ifconfig, netstat)
- Scan output and documentation (file export)
- Full penetration testing reconnaissance methodology

---

## Screenshots

| File | Description |
|------|-------------|
| `a.png` | ifconfig — network interface configuration on Kali Linux |
| `b.png` | netstat -na — active connections and listening ports |
| `c.png` | nmap -sn — ping sweep discovering 4 live hosts |
| `d.png` | nmap -Pn — port scan across all live hosts |
| `e.png` | nmap -sS — stealth SYN scan results |
| `f.png` | nmap -sT — full TCP connect scan |
| `g.png` | nmap -F — fast scan of common ports |
| `h.png` | nmap -sU and nmap -A — UDP and aggressive scan with service versions |
| `j.png` | nmap -A continued — MySQL, PostgreSQL, Samba, VNC details |
| `l.png` | nmap -sS -oS — scan results exported to kiddie.txt |

---

*All scanning was performed in an isolated virtual lab environment for educational purposes only. No real systems were targeted.*
