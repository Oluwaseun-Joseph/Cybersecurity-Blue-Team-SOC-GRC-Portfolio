<h1>Credentialed Vulnerability Assessment of a Kali Linux VM Using Nessus in a Home Lab</h1>


<h2>Description</h2>
In this project, I performed a credentialed vulnerability scan on a Kali Linux virtual machine as part of a home lab setup. Using Tenable’s Nessus Essentials, I configured SSH-based credentials to allow deeper access to the system, enabling more accurate detection of vulnerabilities in services like Node.js, PostgreSQL, and Python libraries.
<br />


<h2>Lab Environment</h2>
- <b>Operating System: Kali Linux (Kernel 6.12.25-amd64)</b> 
- <b>Tool: Nessus Essentials v10.8.3</b> 
- <b>Scan Type: Credentialed SSH Scan</b> 
- <b>Target IP: 10.0.2.15</b> 

<h2> Goals </h2>


- <b>Discover known vulnerabilities affecting installed packages</b> 
- <b>Analyze their severity using CVSS scores</b> 
- <b>Provide patching or remediation steps</b> 
- <b>Demonstrate real-world vulnerability management skills</b> 

<h2>Scan Summary</h2>

<p align="center">
Overall Scan Result <br/>
<img src="https://imgur.com/bDuA58E.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />
  
<p align="center">
Key Vulnerabilities found in Node.js <br/>
<img src="https://imgur.com/G2ScYh1.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />
  
<p align="center">
Key Vulnerabilities found in PostgreSQL <br/>
<img src="https://imgur.com/ds2HGva.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />

<p align="center">
Vulnerability found in Tenable Nessus <br/>
<img src="https://imgur.com/bNXgzQd.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />

<p align="center">
Vulnerability found in Tornadoweb <br/>
<img src="https://imgur.com/7MJH42r.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />

<p align="center">
Vulnerability found in SSL <br/>
<img src="https://imgur.com/DqRJgDD.png" height="90%" width="80%" alt="Credentialed Vulnerability Assessment"/>
<br />

<h2>Key Vulnerabilties Found</h2>

- <b>CVE-2024-21892 (Critical): Privilege escalation in Node.js</b> 
- <b>CVE-2024-27980 (High): Command injection via batch handling in Node.js</b> 
- <b>CVE-2023-5869 (High): Memory overflow in PostgreSQL</b> 
- <b>CVE-2024-4317 (Medium): PostgreSQL information disclosure via extended statistics</b>

<h2>Recommended Fixes</h2>

- <b>Upgrade Node.js to v20.19.2 or later</b> 
- <b>Update PostgreSQL to version 16.7 or higher</b> 
- <b>Patch Tornado library to v6.5.0</b> 
- <b>Replace self-signed SSL certificates with trusted CA-signed certs</b> 

<h2>Skills Demonstrated</h2>

- <b>Secure configuration of credentialed scans using SSH</b>
- <b>CVE research and prioritization using CVSS</b>
- <b>Real-world remediation planning and report writing</b>
- <b>Familiarity with Linux file systems and vulnerability scanning practices</b>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
