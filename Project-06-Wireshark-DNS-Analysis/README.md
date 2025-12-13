# Project 05 – Wireshark DNS Analysis: Resolution Flow, Caching & Packet Forensics

## Overview
In this project, I analyzed Domain Name System (DNS) behavior by combining `nslookup` diagnostics with packet-level inspection in Wireshark. I focused on how DNS queries are generated, how responses are returned, how caching affects resolution, and how DNS directly enables HTTP and HTTPS connections.

This analysis was conducted from a defensive and forensic perspective, mirroring how SOC analysts investigate DNS activity during incident response and network troubleshooting.

> 📌 **Screenshot Reference:**  
> All screenshots referenced below are stored in the `/Screenshots` directory and use descriptive filenames for clarity and traceability.

---

## Lab Environment
- **Operating System:** Windows 10  
- **Tools:** Wireshark, nslookup  
- **Protocols Observed:** DNS (UDP/53), HTTP, HTTPS  
- **Preparation:** Local DNS and browser cache cleared prior to capture  

---

## DNS Record Enumeration
Using `nslookup`, I queried DNS servers to retrieve A records and NS records, confirming authoritative responses and resolver behavior.

📸 `Screenshots/dns-nslookup-basic.png`  
📸 `Screenshots/dns-nslookup-ns-records.png`

---

## Cache Reset and Validation
Before capturing traffic, I flushed the local DNS cache and browser cache to ensure all observed DNS queries were fresh network requests.

📸 `Screenshots/dns-cache-flush.png`  
📸 `Screenshots/browser-cache-clear.png`

---

## Wireshark DNS Capture
I initiated a packet capture in Wireshark and generated DNS traffic through both browser access and manual lookups.

📸 `Screenshots/wireshark-dns-capture-start.png`  
📸 `Screenshots/wireshark-dns-packet-trace.png`

---

## DNS Query and Response Analysis
The initial DNS query was sent over UDP to the local resolver and followed by a corresponding response containing the resolved IP address.

📸 `Screenshots/dns-query-initial.png`  
📸 `Screenshots/dns-response-ip-resolution.png`

---

## Transport Layer Behavior
DNS traffic consistently used ephemeral source ports with destination port 53, with the response reversing the port pairing.

📸 `Screenshots/dns-transport-ports.png`

---

## DNS Message Structure
I analyzed DNS header fields, including flags, question count, and answer count, to understand how DNS messages are constructed.

📸 `Screenshots/dns-query-header-fields.png`  
📸 `Screenshots/dns-response-header-fields.png`

---

## DNS and HTTP Correlation
Once the DNS response was received, the browser immediately issued an HTTP GET request. A subsequent redirect transitioned traffic to HTTPS.

📸 `Screenshots/http-get-after-dns.png`  
📸 `Screenshots/http-to-https-redirect.png`

Cached DNS information prevented redundant DNS lookups for additional resources.

📸 `Screenshots/dns-cache-hit.png`

---

## External Resolver Validation
To compare resolver behavior, I performed DNS lookups using Google DNS (8.8.8.8), bypassing local caching.

📸 `Screenshots/dns-google-resolver-query.png`  
📸 `Screenshots/dns-google-resolver-response.png`

---

## Authoritative Name Server Discovery
DNS NS record queries revealed the authoritative name servers for the domain.

📸 `Screenshots/dns-ns-authoritative-records.png`

---

## Conclusion
This project provided hands-on experience with DNS resolution, caching behavior, and packet-level analysis. By correlating DNS activity with HTTP and HTTPS traffic, I strengthened my ability to trace network dependencies and interpret resolver behavior — skills essential for SOC analysis, threat hunting, and network defense.

---

## Repository Structure
```
Project-05-Wireshark-DNS-Analysis/
├── README.md
├── Screenshots/
└── Files/
```
