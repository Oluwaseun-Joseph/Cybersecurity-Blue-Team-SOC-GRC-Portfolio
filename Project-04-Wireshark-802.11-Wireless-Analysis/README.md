# Project 04 – Wireshark 802.11 Wireless Analysis  
**Beacon Frames, Authentication, Association & Roaming Behavior**

## Overview
This project presents a **deep analysis of real IEEE 802.11 wireless traffic** captured from a production home Wi-Fi environment. Unlike wired Ethernet analysis, this investigation focuses on **Layer-2 wireless behavior**, including how devices discover access points, authenticate, associate, roam, and recover from failed connection attempts.

Using **Wireshark’s 802.11 protocol dissection**, the project analyzes management, control, and data frames to reconstruct the full lifecycle of a wireless client interacting with multiple access points.

This analysis mirrors real-world **wireless troubleshooting, SOC investigations, and network forensics** scenarios.

---

## Analysis Environment
- **Tool:** Wireshark  
- **Capture File:** `Wireshark_802_11.pcap`  
- **Wireless Standard:** IEEE 802.11g  
- **Observed Access Points:**  
  - `30 Munroe St`  
  - `linksys_ses_24086`  
- **Wireless Host (STA) MAC:** `00:13:02:d1:b6:4f`  
- **Primary AP (BSSID):** `00:16:b6:f7:1d:51`  

---

## Analysis Objectives
- Identify nearby wireless networks via beacon frame analysis  
- Extract BSSID, MAC roles, and supported transmission rates  
- Observe TCP traffic encapsulated within 802.11 frames  
- Analyze deauthentication, DHCP release, and roaming behavior  
- Evaluate failed and successful authentication/association attempts  
- Reconstruct wireless recovery after a roaming failure  

---

## Investigation Walkthrough & Evidence

### Initial Capture Review
The packet capture contains beacon frames, management traffic, and data frames from multiple access points operating on the same channel. This provides visibility into both **intended** and **incidental** wireless traffic.

📁 Evidence: `Screenshots/wifi-startup.png`

---

### Wireless Data Traffic over 802.11
The wireless host initiates two outbound HTTP requests over the Wi-Fi connection:

- **24.82s** → `http://gaia.cs.umass.edu/.../alice.txt`  
- **32.82s** → `http://www.cs.umass.edu`

These requests confirm successful data transmission over the wireless link prior to roaming activity.

📁 Evidence:  
- `Screenshots/http-request-1.png`  
- `Screenshots/http-request-2.png`

---

##  Beacon Frame & Network Discovery Analysis

### Wireless Networks Observed
Beacon frame analysis revealed two access points advertising most frequently during the capture:

- **30 Munroe St**  
- **linksys_ses_24086**

These SSIDs were identified by filtering beacon frames  
(`wlan.fc.type_subtype == 0x08`) and inspecting the SSID parameters.

📁 Evidence: `Screenshots/ssid-list.png`

---

### Beacon Interval Behavior
Both access points broadcast beacon frames at a consistent interval of approximately **0.1024 seconds**, indicating standard beacon timing behavior.

📁 Evidence:  
- `Screenshots/beacon-interval-linksys.png`  
- `Screenshots/beacon-interval-munroe.png`

---

### BSSID & MAC Addressing
- **Beacon Source MAC / BSSID:** `00:16:b6:f7:1d:51`  
- **Beacon Destination MAC:** `ff:ff:ff:ff:ff:ff` (broadcast)

This confirms normal access point advertisement behavior.

📁 Evidence:  
- `Screenshots/source-mac.png`  
- `Screenshots/broadcast-dest.png`  
- `Screenshots/bssid.png`

---

### Supported Transmission Rates
The access point advertises:

- **Standard rates:** 1, 2, 5.5, 11 Mbps  
- **Extended rates:** 6–54 Mbps  

This reflects backward compatibility with legacy clients while supporting higher throughput.

📁 Evidence: `Screenshots/supported-rates.png`

---

##  MAC Roles & TCP over 802.11

802.11 frames encapsulating TCP traffic reveal distinct MAC roles:

| Role | Address |
|---|---|
| Wireless Host (STA) | `00:13:02:d1:b6:4f` |
| Access Point (BSSID) | `00:16:b6:f7:1d:51` |
| First-Hop Router | `00:16:b6:f4:eb:a8` |
| Host IP | `192.168.1.109` |
| Destination IP | `128.119.245.12` |

This demonstrates **Layer-2 forwarding over wireless** with Layer-3 routing beyond the access point.

📁 Evidence:  
- `Screenshots/mac-roles-1.png`  
- `Screenshots/mac-roles-2.png`  
- `Screenshots/mac-roles-3.png`

---

##  SYN/ACK Analysis over Wireless

A TCP SYN/ACK frame carried within 802.11 contains three MAC addresses:

- **Receiver (Destination):** Wireless host  
- **Source:** First-hop router  
- **Transmitter / BSSID:** Access point  

This highlights the distinction between **IP endpoints** and **wireless hop MAC roles**.

📁 Evidence: `Screenshots/synack-mac-analysis.png`

---

##  Disconnection & Roaming Attempt

At **49.58s**, the host intentionally disconnects from `30 Munroe St` by:

1. Sending a **DHCP Release** (IP layer)  
2. Transmitting an **802.11 Deauthentication frame** (MAC layer)  

No disassociation frames were observed, indicating deauthentication alone was used.

📁 Evidence:  
- `Screenshots/dhcp-release.png`  
- `Screenshots/deauth-frame.png`  
- `Screenshots/no-disassoc.png`

---

##  Authentication Failure & Recovery

The host attempts to authenticate with `linksys_ses_24086`:

- **Six authentication frames** sent  
- **Open System Authentication** (no key required)  
- **No SEQ=2 response** received from the AP  

The host subsequently abandons this attempt.

📁 Evidence:  
- `Screenshots/auth-attempts.png`  
- `Screenshots/open-auth.png`  
- `Screenshots/no-auth-response.png`

---

##  Successful Reassociation

At **63.169s**, the host successfully authenticates and associates with  
`30 Munroe St`, completing the wireless recovery process.

📁 Evidence:  
- `Screenshots/failed-auth.png`  
- `Screenshots/successful-auth.png`  
- `Screenshots/assoc-request.png`  
- `Screenshots/assoc-response.png`

---

##  Conclusion
This project demonstrates a **complete end-to-end 802.11 wireless analysis**, including:

- Beacon-based network discovery  
- MAC-layer addressing and roles  
- TCP encapsulation over wireless  
- Deauthentication and DHCP release  
- Failed roaming attempts  
- Successful reassociation and recovery  

The analysis reflects real-world **wireless troubleshooting, SOC monitoring, and network forensics** tasks and builds practical capability in:

- Wireless security analysis  
- Wi-Fi troubleshooting  
- Layer-2 protocol inspection  
- Roaming behavior interpretation  
- Incident reconstruction  

---

## 📂 Repository Structure
```
Project-04-Wireshark-802.11-Wireless-Analysis/
├── Files/
│   └── Wireshark-80211-Wireless-Analysis-Report.pdf
├── Screenshots/
├── Raw_Logs/
│   └── Wireshark_802_11.pcap
└── README.md
```
