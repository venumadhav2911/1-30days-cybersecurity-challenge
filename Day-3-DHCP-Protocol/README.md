# 🌐 Day 3 Challenge — Advanced DHCP Protocol Analysis

## 🎯 Objectives
- Analyze the **DHCP DORA process** (Discover → Offer → Request → ACK).  
- Observe **lease renewal** (Request → ACK).  
- Extract important DHCP options from the ACK packet.  
- Understand **security risks** of DHCP and how to defend against them.  

---

## 🧪 Lab Setup
- **Environment:** Kali Linux VM (interface `eth0`)  
- **Tools Used:** Wireshark, Linux CLI (`dhclient`, `ip`)  
- **Server:** VirtualBox NAT DHCP server (`10.0.2.2`)  

---

## 🔄 DHCP Workflow

```mermaid
sequenceDiagram
    participant Client
    participant Server

    Client->>Server: DHCP Discover (Broadcast)
    Server->>Client: DHCP Offer (Proposed IP)
    Client->>Server: DHCP Request (Accepts IP)
    Server->>Client: DHCP ACK (Lease Granted)

    Note over Client,Server: Renewal (T1 time ~50% lease)<br>Request → ACK only
# Packet Captures
1. DORA Process

2. Lease Renewal

3. DHCP ACK Options

 ->Server Identifier → 10.0.2.2

 ->Subnet Mask → 255.255.255.0

 ->Router (Gateway) → 10.0.2.2

 ->DNS Server → 10.0.2.3

 ->Lease Time → 86400 seconds (1 day)

4. Linux Verification

 ->Confirmed DHCP-assigned IP with:

 ->ip a show eth0

🔐 Security Analysis
🚨 DHCP Attacks

Rogue DHCP Server → Fake offers with malicious gateway/DNS → MITM/phishing.

DHCP Starvation → Flood Discover messages to exhaust pool → DoS.

🛡️ Defenses

DHCP Snooping (switch feature to block rogue servers).

Port Security / Rate Limiting → prevent starvation.

IDS/IPS / SIEM Monitoring → detect abnormal DHCP behavior.

✅ Key Takeaways

DHCP automates IP assignment using DORA.

Lease renewals save traffic by skipping Discover/Offer.

DHCP ACK options define network parameters (mask, DNS, gateway).

DHCP misconfigurations or attacks can compromise the whole LAN.
