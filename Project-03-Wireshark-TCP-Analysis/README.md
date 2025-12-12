# Project 03 – Wireshark TCP Analysis: File Upload, Segmentation & RTT Measurement

## Overview
This project analyzes how TCP ensures reliable delivery by capturing the upload of a 150 KB file (**alice.txt**) from a local Windows computer to the server **gaia.cs.umass.edu**. Using Wireshark, I examined:

- The TCP three-way handshake  
- Sequence and acknowledgment numbers  
- TCP segmentation of a large HTTP POST  
- Flow control using the receiver-advertised window  
- Congestion control behaviors  
- Retransmission detection  
- Round-trip time (RTT) measurements  

This project demonstrates strong packet analysis skills and a deep understanding of TCP reliability and performance mechanisms.

---

## Lab Environment
- **Operating System:** Windows 10  
- **Tool:** Wireshark (latest version)  
- **Protocol:** TCP  
- **Server:** gaia.cs.umass.edu  
- **File Uploaded:** `alice.txt` (150 KB)  
- **Network:** Wi-Fi  

---

## Objectives
1. Capture a TCP file upload to a remote server  
2. Identify handshake packets (SYN, SYN/ACK, ACK)  
3. Analyze segmentation of large HTTP POST data  
4. Trace sequence and acknowledgment numbers  
5. Measure TCP RTT  
6. Evaluate receiver-advertised window values  
7. Check for retransmissions  

---

# 📌 **Implementation & Evidence**

### 1. Downloading *Alice in Wonderland*  
URL used:  
http://gaia.cs.umass.edu/wireshark-labs/alice.txt  
 `Screenshots/alice-download.png`

### 2. Navigating to the Upload Page  
📸 `Screenshots/tcp-upload-page.png`

### 3. Starting the Wireshark Capture  
📸 `Screenshots/wireshark-start-capture.png`

### 4. Uploading the File (HTTP POST Triggered)  
📸 `Screenshots/upload-confirmation.png`

---

# 📘 **Questions & Analysis (Numbered and Structured)**

---

## **Question 1 — Client IP & Port**
📌 **Findings:**  
- Client IP: `10.166.239.226`  
- Client Port: `62381`  

📸 Screenshot: `Screenshots/client-ip-port.png`

---

## **Question 2 — Server IP & Port**
📌 **Findings:**  
- Server IP: `128.119.245.12`  
- Server Port: `80`  

📸 Screenshot: `Screenshots/server-ip-port.png`

---

## **Question 3 — Identifying the SYN Segment**
📌 The SYN segment contains:  
- Raw sequence number: `2777201873`  
- Relative sequence: `0`  
- Flag: SYN  

📸 Screenshot: `Screenshots/syn-segment.png`

---

## **Question 4 — Identifying the SYN/ACK Segment**
📌 The SYN/ACK includes:  
- Server Initial Sequence: `2276437536`  
- Acknowledgment Number: `996038718`  
- Flags: **SYN + ACK**

📸 Screenshot: `Screenshots/synack-segment.png`

---

## **Question 5 — TCP Segment Containing the HTTP POST**
📌 For **Packet #306**:  
- Raw sequence number: `996381015`  
- Relative sequence: `1`  
- Payload size: `721 bytes`  
- The full upload did **not** fit in a single segment  

📸 Screenshot: `Screenshots/http-post-segment.png`

---

## **Question 6 — RTT Measurements**

### RTT for First Segment  
- Send: `15:46:03.131396000`  
- ACK: `15:46:03.158948000`  
- **RTT ≈ 27.552 ms**

📸 `Screenshots/rtt-segment-1.png`

### RTT for Second Segment  
- Send: `15:46:03.133258`  
- ACK: `15:46:03.161104`  
- **RTT ≈ 27.846 ms**

📸 `Screenshots/rtt-segment-2.png`

---

## **Question 7 — Segment Sizes (Header + Payload Breakdown)**

| Segment | Frame | Header | Payload | Total |
|---------|--------|---------|----------|--------|
| 1 | 306 | 20 B | 721 B | 741 B |
| 2 | 315 | 20 B | 11,250 B | 11,270 B |
| 3 | 316 | 20 B | 1,250 B | 1,270 B |
| 4 | 338 | 20 B | 2,500 B | 2,520 B |

📸 Screenshots:  
- `Screenshots/segment1-size.png`  
- `Screenshots/segment2-size.png`  
- `Screenshots/segment3-size.png`  
- `Screenshots/segment4-size.png`

---

## **Question 8 — Minimum Advertised Window (Flow Control)**

| Data Segment | ACK Frame | Advertised Window |
|--------------|------------|-------------------|
| 1 | 335 | 30,720 B |
| 2 | 337 | 33,664 B |
| 3 | 339 | 43,648 B |
| 4 | 340 | 53,632 B |

📌 **Minimum Advertised Window:** 30,720 bytes  
📌 Sender was **never throttled**.

📸 Screenshots:  
`Screenshots/window-335.png`  
`Screenshots/window-337.png`  
`Screenshots/window-339.png`  
`Screenshots/window-340.png`

---

## **Question 9 — Retransmission Check**
Using:  
`tcb.analysis.retransmission`

📌 **Result:** No retransmissions occurred.  
The connection was stable and clean.

📸 Screenshot: `Screenshots/no-retransmissions.png`

---

# 🧾 Conclusion
This project provided hands-on insight into how TCP maintains reliable, ordered delivery during a file upload. Through analyzing handshake behavior, segmentation patterns, acknowledgments, congestion control signals, RTT values, and flow control, I gained practical understanding of real-world TCP performance.

Skills demonstrated include:

- Packet inspection using Wireshark  
- Sequence/ACK number interpretation  
- Flow control and congestion control analysis  
- RTT computation  
- Large payload segmentation tracing  
- Applying filters to isolate protocol events  

---

# 📁 Repository Structure

```
Project-03-Wireshark-TCP-Analysis/
├── README.md
├── Screenshots/
│ ├── alice-download.png
│ ├── tcp-upload-page.png
│ ├── wireshark-start-capture.png
│ ├── upload-confirmation.png
│ ├── tcp-segmentation.png
│ ├── tcp-handshake.png
│ ├── client-ip-port.png
│ ├── server-ip-port.png
│ ├── syn-segment.png
│ ├── synack-segment.png
│ ├── http-post-segment.png
│ ├── rtt-segment-1.png
│ ├── rtt-segment-2.png
│ ├── segment1-size.png
│ ├── segment2-size.png
│ ├── segment3-size.png
│ ├── segment4-size.png
│ ├── window-335.png
│ ├── window-337.png
│ ├── window-339.png
│ ├── window-340.png
│ └── no-retransmissions.png
└── Files/
└── Lab-02-Wireshark-TCP-Report.pdf
```
