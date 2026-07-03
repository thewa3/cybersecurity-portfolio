# 🔍 Wireshark Network Traffic Analysis

## Overview
This project documents my hands-on practice with Wireshark — one of the most widely used network protocol analyzers in cybersecurity. Using my home lab environment, I captured and analyzed live network traffic to understand how data moves across a network and how to identify suspicious activity.

---

## What I Did

- Installed and configured Wireshark on a Windows machine
- Captured live HTTP network traffic from my virtual lab environment
- Analyzed real packet data including GET requests and server responses
- Identified HTTP response codes including 301 Moved Permanently and 200 OK
- Tracked communication between IP addresses (source: 192.168.1.10 and destination servers)
- Configured Wireshark plugin directories for custom Lua script integration

---

## Skills Demonstrated

| Skill | Description |
|-------|-------------|
| **Packet Capture** | Capturing live HTTP traffic on a network interface |
| **Traffic Analysis** | Reading GET requests, redirects, and server responses |
| **Protocol Identification** | Identifying HTTP/1.1 traffic and response codes |
| **Plugin Configuration** | Setting up Wireshark personal plugin directory for custom scripts |
| **Network Forensics** | Understanding what normal vs suspicious traffic looks like |

---

## Real Traffic Captured

From the packet capture, I was able to identify:
- **HTTP GET requests** to /online and /favicon.ico endpoints
- **301 Moved Permanently** redirect responses (text/html)
- **200 OK** successful responses including PNG image files
- Communication between local IP **192.168.1.10** and external web servers
- Packet sizes ranging from 273 to 639 bytes

---

## Tools Used

- Wireshark (Windows)
- Virtual Lab Network (isolated environment)
- Lua scripting (for plugin development — see Project 3)

---

## Screenshots

| Screenshot | Description |
|-----------|-------------|
| `wireshark-folders.png` | Wireshark plugin directory structure showing personal and global plugin paths |
| `wireshark-http-capture.png` | Live HTTP traffic capture showing GET requests and server responses |

---

*All traffic captured in an isolated virtual lab environment for educational purposes only.*
