# Project 03 – Wireshark TCP Analysis: File Upload, Segmentation & RTT Measurement

## 📌 Overview

This project analyzes how the **Transmission Control Protocol (TCP)** ensures reliable data delivery
by capturing and inspecting a real file upload using **Wireshark**.

A ~150 KB text file (*Alice’s Adventures in Wonderland*) was uploaded from a client machine to the
remote server **gaia.cs.umass.edu**, and the full packet exchange was captured and analyzed.
The investigation focuses on:

- TCP three-way handshake
- Sequence and acknowledgment numbers
- TCP segmentation
- Receiver-advertised window (flow control)
- Round-trip time (RTT) measurement
- Retransmission verification

This project demonstrates **packet-level network analysis skills** relevant to SOC, Blue Team,
and Network Security roles.

> 📌 **Note:** All screenshots referenced below are stored in the `/Screenshots` directory
> and are named to match their corresponding figure numbers for traceability.

---

##  Lab Environment

- **Operating System:** Windows 10  
- **Tool:** Wireshark  
- **Protocol Analyzed:** TCP / HTTP  
- **Server:** gaia.cs.umass.edu  
- **File Uploaded:** `alice.txt` (~150 KB)  
- **Network Type:** Wi-Fi  

---

##  Objectives

- Capture a real TCP file upload
- Observe the TCP three-way handshake
- Analyze TCP sequence & acknowledgment numbers
- Examine TCP segmentation behavior
- Measure RTT from packet timestamps
- Validate whether retransmissions occurred

---

## 🔬 Investigation Walkthrough

### Step 1: Downloading the File

The ASCII version of *Alice’s Adventures in Wonderland* was downloaded from the UMass Wireshark lab site.

**Figure 1 – Browser accessing `alice.txt`**  
📁 Screenshot file: `alice-download.png`

**Figure 2 – Saving `alice.txt` locally**  
📁 Screenshot file: `alice-save-dialog.png`

---

### Step 2: Navigating to the Upload Page

The TCP upload page was accessed to prepare for uploading the file.

 **Figure 3 – TCP upload page on gaia.cs.umass.edu**  
📁 Screenshot file: `tcp-upload-page.png`

---

### Step 3: Selecting the File

The previously downloaded `alice.txt` file was selected using the Browse button.

**Figure 4 – Selecting the `alice.txt` file**  
📁 Screenshot file: `file-selection.png`

---

### Step 4: Starting Packet Capture

Wireshark packet capture was started before initiating the upload.

 **Figure 5 – Wireshark capture started**  
📁 Screenshot file: `wireshark-start-capture.png`

---

### Step 5: Uploading the File

The file upload was initiated and confirmed as successful.

 **Figure 6 – Upload confirmation message**  
📁 Screenshot file: `upload-confirmation.png`

---

##  Packet Analysis

### HTTP POST Inspection & Segmentation

The captured trace was inspected to locate the HTTP POST request responsible for uploading
`alice.txt`.

 **Figure 7 – Expanded HTTP POST request**  
📁 Screenshot file: `http-post-expanded.png`

The POST payload exceeded a single TCP segment and was therefore segmented.

**Figure 8 – TCP segment containing start of POST payload**  
📁 Screenshot file: `tcp-segmentation.png`

---

### TCP Handshake Observation

A TCP display filter was applied to isolate handshake packets.

**Figure 9 – TCP three-way handshake (SYN, SYN/ACK, ACK)**  
📁 Screenshot file: `tcp-handshake.png`

---

##  Findings (Key Questions & Evidence)

### Client & Server Details

 **Figure 10 – Client IP and source port**  
📁 Screenshot file: `client-ip-port.png`

- Client IP: `10.166.239.226`
- Source Port: `62381`

 **Figure 11 – Server IP and destination port**  
📁 Screenshot file: `server-ip-port.png`

- Server IP: `128.119.245.12`
- Destination Port: `80`

---

### TCP Control Segments

**Figure 12 – Initial TCP SYN segment**  
📁 Screenshot file: `syn-segment.png`

📸 **Figure 13 – SYN/ACK response from server**  
📁 Screenshot file: `synack-segment.png`

---

### HTTP POST Segment Details

**Figure 14 – TCP segment carrying HTTP POST header**  
📁 Screenshot file: `post-segment.png`

- Payload size: 721 bytes
- File transmitted across multiple TCP segments

---

### RTT Measurement

**Figure 15 – Time POST segment sent**  
📁 Screenshot file: `rtt-post-send.png`

**Figure 16 – ACK received for POST segment**  
📁 Screenshot file: `rtt-post-ack.png`

- RTT ≈ **27.55 ms**

**Figure 17 – Second data segment sent**  
📁 Screenshot file: `rtt-second-send.png`

**Figure 18 – ACK received for second segment**  
📁 Screenshot file: `rtt-second-ack.png`

- RTT ≈ **27.85 ms**

---

### TCP Segment Sizes

**Figures 19a–19d – Total length of first four TCP data segments**  
📁 Screenshot files:
- `segment-length-1.png`
- `segment-length-2.png`
- `segment-length-3.png`
- `segment-length-4.png`

---

### Flow Control (Advertised Window)

**Figures 20a–20d – Receiver advertised window sizes**  
📁 Screenshot files:
- `window-30720.png`
- `window-33664.png`
- `window-43648.png`
- `window-53632.png`

- Minimum advertised window: **30,720 bytes**
- Sender was **never throttled**

---

### Retransmission Check

**Figure 21 – Retransmission filter applied**  
📁 Screenshot file: `retransmission-filter.png`

- Result: **No TCP retransmissions detected**

---

## 📁 Project Structure
```
Project-03-Wireshark-TCP-Analysis/
├── Files/
│   └── Project-03-Wireshark-TCP-Analysis-Report.pdf
├── Screenshots/
│   ├── alice-download.png
│   ├── tcp-upload-page.png
│   ├── wireshark-start-capture.png
│   ├── upload-confirmation.png
│   ├── tcp-handshake.png
│   ├── tcp-segmentation.png
│   ├── client-ip-port.png
│   ├── server-ip-port.png
│   ├── syn-segment.png
│   ├── synack-segment.png
│   ├── http-post-segment.png
│   ├── rtt-segment-1.png
│   ├── rtt-segment-2.png
│   ├── segment1-size.png
│   ├── segment2-size.png
│   ├── segment3-size.png
│   ├── segment4-size.png
│   └── no-retransmissions.png
└── README.md
```

---

##  Skills Demonstrated

- Network packet analysis (Wireshark)
- TCP protocol internals
- RTT and performance measurement
- Evidence-based investigation
- SOC-style documentation
- GitHub portfolio structuring

---

##  Conclusion

This project provides a real-world demonstration of TCP reliability mechanisms using
packet-level evidence. By capturing and analyzing a live file upload, the project validates
how TCP establishes connections, segments data, manages flow control, and ensures reliable
delivery without retransmissions.

This analysis reflects skills directly applicable to **SOC Analyst, Network Security,
and Blue Team roles**.
```
