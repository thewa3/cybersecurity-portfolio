# 🚨 HTTP Traffic Alert — Custom Wireshark Lua Plugin

## Overview
This project involved writing a custom Lua script plugin for Wireshark that automatically triggers an alarm whenever HTTP traffic is detected on the network. This demonstrates both network analysis skills and the ability to write custom security monitoring tools.

---

## What I Built

I wrote a Lua script called `http_alarm.lua` and installed it into Wireshark's personal plugins directory. The script monitors live network traffic and fires an alert notification whenever it detects HTTP protocol activity.

---

## How It Works

1. Wireshark loads the `http_alarm.lua` plugin automatically on startup
2. The script monitors all captured packets in real time
3. When an HTTP packet is detected, the alarm triggers
4. This simulates a basic **Intrusion Detection System (IDS)** — a real tool used by SOC analysts

---

## Technical Details

| Detail | Value |
|--------|-------|
| **Script name** | `http_alarm.lua` |
| **Script type** | Lua script |
| **Plugin location** | `C:\Users\Ashley\AppData\Roaming\Wireshark\plugins\http_alarm.lua` |
| **Trigger condition** | Any HTTP protocol traffic detected |
| **Alert type** | Real-time notification/alarm |

---

## Skills Demonstrated

- **Lua scripting** — writing a functional plugin from scratch
- **Wireshark plugin development** — installing and configuring custom scripts
- **Protocol filtering** — targeting specific traffic types (HTTP)
- **Security monitoring logic** — building alert conditions based on network behavior
- **IDS concepts** — understanding how real intrusion detection systems work

---

## Why This Project Matters

Most cybersecurity professionals use tools that already exist. Building a custom detection tool shows a deeper level of understanding — you're not just using security tools, you're creating them. This is exactly the kind of initiative that stands out to employers.

---

## Screenshots

| Screenshot | Description |
|-----------|-------------|
| `http-alarm-plugin-file.png` | The http_alarm.lua file saved in Wireshark personal plugins folder |
| `wireshark-http-capture.png` | HTTP traffic being captured that would trigger the alarm |

---

*Built in an isolated virtual lab environment for educational purposes only.*
