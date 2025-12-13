# Project 05 – Wireshark DNS Analysis: Resolution Flow, Caching Behavior & Packet Forensics

## Overview
This project provides a complete analysis of DNS resolution behavior by combining `nslookup` diagnostics with packet-level inspection in Wireshark. Through controlled lookups, cache resets, and real web browsing, I traced how DNS queries and responses flow across the network, how caching affects performance, and how DNS precedes HTTP/HTTPS connections.

My goal was to analyze DNS from a **forensic and operational perspective**, focusing on:
- How hostnames are resolved into IP addresses  
- Differences between authoritative and cached responses  
- UDP port usage in DNS transactions  
- DNS message structure (flags, questions, answers, authorities, additionals)  
- How DNS resolution directly triggers HTTP/HTTPS requests  
- The impact of browser redirects (HTTP → HTTPS) on DNS behavior  

This project strengthens foundational skills required for SOC analysts, network defenders, and cybersecurity engineers.

> 🔎 **Screenshot Reference:**  
> All images used in this analysis are stored in the `/Screenshots` folder and follow consistent naming aligned with each analysis section.

---

## Lab Environment
- **Operating System:** Windows 10  
- **Tools:** Wireshark, nslookup  
- **Protocols Observed:** DNS over UDP (port 53), HTTP/HTTPS  
- **Preparation:** Local DNS cache cleared to ensure fresh, uncached lookups  

---

## Key Activities Performed

### 1. DNS Record Enumeration Using nslookup  
I used `nslookup` to retrieve:
- Type A (IPv4) records  
- NS (authoritative nameserver) records  
- Reverse lookup information  

These tests revealed authoritative vs non-authoritative responses and validated which DNS servers were handling the queries.

📸 `Screenshots/nslookup-basic.png`  
📸 `Screenshots/nslookup-NS-record.png`

---

### 2. DNS Cache Reset & Verification  
Before packet capture, I flushed the DNS cache to ensure that all subsequent lookups were fresh network queries rather than cached results.

📸 `Screenshots/clear-dns-cache.png`  
📸 `Screenshots/clear-browser-cache.png`

---

### 3. Capturing DNS Traffic in Wireshark  
With the cache cleared, I launched Wireshark and observed the complete DNS resolution workflow during:
- Manual `nslookup` commands  
- Navigation to http://gaia.cs.umass.edu  
- Automatic browser redirects and follow-up requests  

📸 `Screenshots/wireshark-capture-start.png`  
📸 `Screenshots/wireshark-dns-trace.png`

---

# 📘 **DNS Forensic Analysis**

## **Initial DNS Lookup Identification**  
The first DNS request for `gaia.cs.umass.edu` appeared in **Frame 169**, sent over **UDP port 53** to the local DNS resolver (`10.30.1.158`).  
The response was captured in **Frame 224**, verifying the pair.

📸 `Screenshots/q5-first-dns-query.png`  
📸 `Screenshots/q6-dns-response.png`

---

## **Transport Layer Behavior (Ports & Protocols)**  
DNS queries consistently used:
- **Source ports:** ephemeral high-range  
- **Destination port:** 53 (DNS service port)  

Responses inverted the port pairing as expected.

📸 `Screenshots/q7a-query-port.png`  
📸 `Screenshots/q7b-response-port.png`

---

## **DNS Resolver Flow & Destination Server Analysis**  
All DNS queries were directed to **10.30.1.158**, which served as the local forwarding resolver.

This confirmed the path:
**Client → Local Resolver → Authoritative DNS (upstream)**

📸 `Screenshots/q8-destination-ip.png`

---

## **DNS Message Structure Breakdown**  
During packet inspection, I analyzed DNS header fields including:
- Flags (query/response, recursion desired, recursion available)  
- Question count  
- Answer count  
- Authority and additional record sections  

Examples showed:
- Queries containing **1 question** and **0 answers**  
- Responses containing **1 question** and **1 or more answers**

📸 `Screenshots/q9-dns-query-fields.png`  
📸 `Screenshots/q10-dns-response-fields.png`

---

## **Correlation Between DNS Resolution and HTTP/HTTPS Traffic**  
After DNS returned the IP address (`128.119.245.12`), the browser immediately initiated an HTTP GET request (Frame 232).

📸 `Screenshots/q11a-http-get.png`

### **DNS → HTTP Flow Observations**
- First DNS A-record query appeared in Frame 170  
- DNS response appeared in Frame 221  
- Once resolved, no additional DNS queries were required  

📸 `Screenshots/q11b-dns-query.png`  
📸 `Screenshots/q11c-dns-response.png`

### **HTTPS Redirect Behavior**
A redirect (Frame 236) transitioned the session from HTTP to HTTPS, meaning subsequent resource requests were encrypted and not visible as GET requests in cleartext.

📸 `Screenshots/q11d-redirect-https.png`

### **DNS Caching Impact**
The browser did **not** issue a second DNS lookup for image files because the hostname was already cached.

📸 `Screenshots/q11e-dns-cache.png`

---

## **Port Behavior Verification in Additional Lookups**  
Additional DNS lookups showed consistent use of:
- Destination: **port 53**  
- Source: ephemeral port  
- Reverse direction on response  

📸 `Screenshots/q12-dns-port.png`  
📸 `Screenshots/q12-dns-response-port.png`

---

## **Type A Lookup for www.cs.umass.edu**  
Captured queries showed:
- Request type: **A record**  
- No answers initially (queries section only)  

📸 `Screenshots/q14-type-a.png`

Response packets contained:
- **1 A-record answer**  
- IP address resolution confirming successful lookup  

📸 `Screenshots/q15-response-count.png`

---

## **Use of Google DNS (8.8.8.8) for Independent Validation**  
Queries were repeated using Google DNS to bypass institutional caching and compare resolution paths.

📸 `Screenshots/q16-google-dns.png`  
📸 `Screenshots/q17-query-count.png`

---

## **NS Record Enumeration and Authority Discovery**  
Inspection revealed:
- **3 NS records** returned  
- Names of authoritative nameservers for `umass.edu`  
- Zero additional records in this particular exchange  

📸 `Screenshots/q18-ns-records.png`

---

# 🧾 Conclusion
This DNS analysis provided a complete end-to-end view of how hostnames are resolved and how DNS interacts with upper-layer protocols such as HTTP and HTTPS.

Through packet forensics and resolver testing, I strengthened my ability to:
- Trace DNS transactions at the packet level  
- Interpret query/response pairs  
- Understand caching and its effect on network traffic  
- Analyze authoritative vs non-authoritative response behavior  
- Correlate DNS resolution with web traffic sequences  
- Use Wireshark for DNS troubleshooting and investigation  

These are foundational skills for SOC analysts, incident responders, penetration testers, and network engineers.

---
