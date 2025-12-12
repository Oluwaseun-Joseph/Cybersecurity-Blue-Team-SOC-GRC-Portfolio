# Project 04 – Wireshark 802.11 Wireless Analysis (Beacon, Authentication, Association & Roaming)

## Overview
This project analyzes **real Wi-Fi (802.11) wireless traffic** captured from a home network.  
Unlike wired Ethernet captures, this analysis reveals how Wi-Fi devices:

- Discover access points  
- Interpret beacon frames  
- Authenticate & associate  
- Exchange MAC-layer control frames  
- Send data over wireless  
- Roam between access points  
- Attempt connections that fail  

Using **Wireshark’s 802.11 dissection**, this project examines management, control, and data frames to understand real wireless behavior in production environments.

---

## Lab Environment
- **Tool:** Wireshark  
- **Traffic Source:** Provided `Wireshark_802_11.pcap` capture  
- **Standard:** IEEE 802.11g  
- **APs observed:**  
  - `30 Munroe St`  
  - `linksys_ses_24086`  
- **Host MAC:** `00:13:02:d1:b6:4f`  
- **AP MAC:** `00:16:b6:f7:1d:51`  

---

## Objectives
1. Identify SSIDs and beacon frame properties  
2. Extract BSSID, supported speeds, and MAC roles  
3. Analyze SYN/SYN-ACK TCP traffic inside 802.11 frames  
4. Understand disassociation, deauthentication, and DHCP release events  
5. Follow an AP-roaming attempt and failure  
6. Analyze authentication and association sequences  

---

## Implementation & Screenshots

### **1. Opening the 802.11 Packet Capture**
Initial Wireshark view showing all wireless beacon, management, and data frames.  
📌 Screenshot: `Screenshots/wifi-startup.png`

### **2. HTTP Requests Over Wireless**
The host performs two HTTP GET requests at:  
- **24.82s** → `http://gaia.cs.umass.edu/.../alice.txt`  
- **32.82s** → `http://www.cs.umass.edu`  

📌 Screenshots:  
`Screenshots/http-request-1.png`  
`Screenshots/http-request-2.png`

### **3. Roaming Attempt**
At **49.58s**, the host disconnects from `30 Munroe St` and tries connecting to `linksys_ses_24086` unsuccessfully.

📌 Screenshots:  
`Screenshots/roam-attempt.png`  
`Screenshots/failed-association.png`

### **4. Reconnecting Successfully**
At **63.0s**, the host re-associates with `30 Munroe St`.

📌 Screenshot:  
`Screenshots/reassociate-success.png`

---

# 🔎 Part 1 — Beacon Frame Analysis

### **Q1. SSIDs Observed**
From page 5 of the report:  
- `30 Munroe St`  
- `linksys_ses_24086`  
📌 Screenshot: `Screenshots/ssid-list.png`

### **Q2. Beacon Interval**
Both APs broadcast beacons at **0.1024 seconds**.  
📌 Screenshots:  
`Screenshots/beacon-interval-linksys.png`  
`Screenshots/beacon-interval-munroe.png`

### **Q3. Source MAC of 30 Munroe St**
From page 7:  
- **Source MAC:** `00:16:b6:f7:1d:51`  
📌 Screenshot: `Screenshots/source-mac.png`

### **Q4. Destination MAC in Beacon**
Always broadcast:  
`ff:ff:ff:ff:ff:ff`  
📌 Screenshot: `Screenshots/broadcast-dest.png`

### **Q5. BSSID**
- **BSSID:** `00:16:b6:f7:1d:51`  
📌 Screenshot: `Screenshots/bssid.png`

### **Q6. Supported Data Rates**
Standard rates: **1, 2, 5.5, 11 Mbps**  
Extended rates: **6–54 Mbps**  
📌 Screenshot: `Screenshots/supported-rates.png`

---

# 🛰️ Part 2 — MAC Address Roles & TCP Frames

### **Q7. MAC Addresses in 802.11 Frames**
From pages 10–13:

| Role | Address |
|------|---------|
| Destination MAC | `00:16:b6:f4:eb:a8` |
| Source MAC | `00:13:02:d1:b6:4f` |
| BSSID | `00:16:b6:f7:1d:51` |
| First-hop router | `00:16:b6:f4:eb:a8` |
| Wireless host MAC | `00:13:02:d1:b6:4f` |
| Host IP | `192.168.1.109` |
| Destination IP | `128.119.245.12` |

📌 Screenshots (Figures 12a–12f):  
`Screenshots/mac-roles-1.png`  
`Screenshots/mac-roles-2.png`  
`Screenshots/mac-roles-3.png`  

---

# 🔁 Part 3 — SYN/ACK Wireless Frame Breakdown

### **Q8. SYN/ACK Three MAC Fields**
From page 14–16:

- Receiver MAC = Destination = `00:13:02:d1:b6:4f`  
- Source MAC = `00:16:b6:f4:eb:a8`  
- Transmitter/BSSID = `00:16:b6:f7:1d:51`

📌 Screenshots:  
`Screenshots/synack-mac-analysis.png`

---

# 🔌 Part 4 — Disconnection & Deauthentication

### **Q9. Host Performs DHCP Release + Deauth**
At **49.58s**, host ends session:

1. **DHCP Release** (IP layer)  
2. **802.11 Deauthentication frame** (MAC layer)  

📌 Screenshots:  
`Screenshots/dhcp-release.png`  
`Screenshots/deauth-frame.png`

It finds **no disassociation frames**, confirming only deauth was sent.  
📌 `Screenshots/no-disassoc.png`

---

# 🔐 Part 5 — Authentication Attempts

### **Q10. Authentication Attempts to linkys_ses_24086**
From page 20:

- **Six authentication frames sent** by host  
- Using filter:  
wlan.fc.type == 0 && wlan.fc.subtype == 11 && wlan.addr == 00:13:02:d1:b6:4f

yaml
Copy code

📌 Screenshot: `Screenshots/auth-attempts.png`

### **Q11. Key Requirement**
The host uses **Open System Authentication**, requiring no key.  
📌 Screenshot: `Screenshots/open-auth.png`

### **Q12. Missing AP Response**
The AP did **not** send Authentication SEQ=2.  
📌 Screenshot: `Screenshots/no-auth-response.png`

---

# 🔄 Part 6 — Successful Reconnection & Association

### **Q13: Failed Authentication to one AP; Success with another**
- Host attempted with MAC `f5:ba:bb` (failed)  
- Later associated with `00:16:b6:f7:1d:51` at **63.169s**

📌 Screenshots:  
`Screenshots/failed-auth.png`  
`Screenshots/successful-auth.png`

### **Q14: Association Frames**
Sequence captured in Frames **2162** and **2166**:

- Association Request  
- Association Response  

📌 Screenshots:  
`Screenshots/assoc-request.png`  
`Screenshots/assoc-response.png`

### **Q15: Transmission Rates Willing to Use**
Host: 1, 2, 5.5, 11 Mbps  
AP: 1–54 Mbps  
📌 Screenshot: `Screenshots/host-rates.png`

---

# 🎯 Conclusion
This project provides a full wireless-protocol analysis at Layer 2 (802.11), demonstrating:

- Beacon frame interpretation  
- MAC-layer addressing roles  
- Authentication & association mechanics  
- DHCP release + deauthentication  
- Wireless roaming failure & recovery  
- TCP encapsulation inside 802.11  

By analyzing these real wireless frames, we build practical skills in:

✔ Wireless forensics  
✔ WiFi troubleshooting  
✔ MAC-layer analysis  
✔ Network security monitoring  
✔ Understanding roaming behavior  

This project strengthens capability for **SOC Analyst**, **Network Security**, and **Wireless Security** roles.

---

# 📂 Repository Structure

Project-04-Wireshark-802.11-Wireless-Analysis/

├── README.md
├── Report/
│   └── Wireshark-80211-Wireless-Analysis-Report.pdf
├── Screenshots/
│   ├── wifi-startup.png
│   ├── http-request-1.png
│   ├── http-request-2.png
│   ├── roam-attempt.png
│   ├── failed-association.png
│   ├── reassociate-success.png
│   ├── ssid-list.png
│   ├── beacon-interval-linksys.png
│   ├── beacon-interval-munroe.png
│   ├── source-mac.png
│   ├── broadcast-dest.png
│   ├── bssid.png
│   ├── supported-rates.png
│   ├── mac-roles-1.png
│   ├── mac-roles-2.png
│   ├── mac-roles-3.png
│   ├── synack-mac-analysis.png
│   ├── dhcp-release.png
│   ├── deauth-frame.png
│   ├── no-disassoc.png
│   ├── auth-attempts.png
│   ├── open-auth.png
│   ├── no-auth-response.png
│   ├── failed-auth.png
│   ├── successful-auth.png
│   ├── assoc-request.png
│   ├── assoc-response.png
│   └── host-rates.png
└── Raw_Logs/
    └── Wireshark_802_11.pcap
