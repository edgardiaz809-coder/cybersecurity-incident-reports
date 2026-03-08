# 🔐 Cybersecurity Incident Report: Network Traffic Analysis

**Google Cybersecurity Certificate · Coursera Portfolio Activity**

![Cybersecurity](https://img.shields.io/badge/Type-Incident_Report-red?style=for-the-badge)
![Protocol](https://img.shields.io/badge/Protocol-DNS_%7C_UDP_%7C_ICMP-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Resolved-green?style=for-the-badge)

---

## 📋 Incident Summary

| Field | Details |
|-------|---------|
| **Incident Type** | DNS Service Outage |
| **Time Detected** | 13:24:32.192571 |
| **Protocols Affected** | DNS, UDP, ICMP |
| **Port Affected** | Port 53 (DNS) |
| **Source IP** | 192.51.100.15 |
| **DNS Server IP** | 203.0.113.2 |
| **Error Returned** | ICMP "Destination Unreachable" |
| **Attempts Made** | 3 consecutive failed attempts |

---

## 🔍 Part 1 — Problem Found in DNS and ICMP Traffic Log

The **UDP protocol** revealed that the DNS server was not listening on **Port 53**. The ICMP echo reply returned a **"Destination Unreachable"** error message on each attempt.

**Protocols & Services Impacted:**
- 🔵 **DNS** (Domain Name System) — Service affected
- 🔵 **UDP** (User Datagram Protocol) — Transport layer used
- 🔵 **ICMP** (Internet Control Message Protocol) — Error reporting

**Most Likely Cause:**
The DNS service was either:
- Not running / crashed on the destination server
- Misconfigured at the application layer
- Actively blocked by a firewall rule on Port 53

---

## 🧠 Part 2 — Analysis & Root Cause

### ⏰ Timeline
The incident began at **13:24:32.192571**. The system attempted the DNS request **three consecutive times**, receiving the same ICMP error each time — confirming a persistent outage rather than a transient glitch.

### 🚨 How the IT Team Detected the Incident
- Automated monitoring tools flagged a series of failed connections before any user reported an issue
- The system triggered a **"three-strike" pattern** — three identical failures in a row
- Log analysis confirmed a persistent outage pointing directly to the DNS service

### 🔎 Investigation Steps Performed

**1. Log Correlation**
Examined network logs to identify failed communication between source `192.51.100.15` and DNS server `203.0.113.2`.

**2. Protocol Analysis**
Used a **Packet Sniffer (Wireshark)** to capture UDP DNS queries and the resulting ICMP "Port Unreachable" error packets — confirming the server was online but Port 53 was inaccessible.

**3. Persistence Verification**
Verified the issue was not a transient glitch by observing **3 repeated identical failures**.

**4. Service Status Check**
Investigated Port 53 to determine if:
- DNS service had stopped or crashed
- A firewall rule was blocking traffic to that port

**5. Root Cause Assessment**
Since the server responded with an ICMP message (confirming network connectivity), the issue was isolated to the **application layer** — the DNS service itself was inaccessible.

### 📌 Key Findings

| Finding | Detail |
|---------|--------|
| Network path | ✅ Clear — server was reachable |
| DNS service | ❌ Not responding on Port 53 |
| Failure pattern | 3 identical ICMP errors — persistent outage |
| Target website | yummyrecipesforme.com — DNS lookup failed |
| Root cause | DNS software crashed or firewall blocking Port 53 |

---

## 💡 What I Learned

- How to read and interpret **ICMP error messages** in network logs
- The difference between a **network-layer issue** vs an **application-layer issue**
- How to use **Wireshark** for packet analysis and protocol investigation
- How **DNS, UDP, and ICMP** interact during a service failure
- The importance of **automated monitoring** for early incident detection

---

## 🛠️ Tools & Concepts Used

![Wireshark](https://img.shields.io/badge/Tool-Wireshark-1679A7?style=flat&logo=wireshark&logoColor=white)
![DNS](https://img.shields.io/badge/Protocol-DNS-orange?style=flat)
![UDP](https://img.shields.io/badge/Protocol-UDP-blue?style=flat)
![ICMP](https://img.shields.io/badge/Protocol-ICMP-red?style=flat)
![Linux](https://img.shields.io/badge/OS-Linux-FCC624?style=flat&logo=linux&logoColor=black)

---

*Portfolio project · [Google Cybersecurity Certificate](https://coursera.org/verify/KW50NYEB4EDG) · Edgar Diaz*
