[README.md](https://github.com/user-attachments/files/29549999/README.md)
# Cyber Security Task 4: Network Intrusion Detection System (NIDS)
**Company:** CodeAlpha  
**Domain:** Cyber Security  

---

## Project Overview
This repository satisfies **TASK 4: Network Intrusion Detection System** from the CodeAlpha cybersecurity curriculum[span_2](start_span)[span_2](end_span). The objective of this project is to implement a rule-based network monitoring signature matrix using **Snort** to inspect live traffic packets, flag anomalous behavior patterns, and generate localized threat triggers[span_3](start_span)[span_3](end_span).

### Repository Structure
* `snort.rules`: Custom signature configuration file mapping specific localized threat triggers.
* `snort3-community.rules`: Official community-vetted signature base protecting against broader network vulnerabilities.
* `README.md`: The complete project overview, deployment breakdown, and live alert analysis report.

---

## Technical Architecture & Detection Signatures

An Intrusion Detection System relies on string evaluation parameters to intercept threat footprints. The signatures implemented in `snort.rules` target common attack steps:

### 1. ICMP Ping Sweep Mapping
* **Rule Logic:** Tracks rapid ICMP echo request behaviors originating from outside configurations.
* **Use Case:** Identifies early attacker reconnaissance phases where adversaries ping devices to map active local hosts.

### 2. Syn Port Scan Tracking
* **Rule Logic:** Evaluates incoming TCP handshakes specifically hunting for isolated Synchronize (`S`) flags that close abruptly before completing the full connection handshake.
* **Use Case:** Detects port discovery scans (e.g., Nmap) tracking down open access ports.

### 3. Application Directory Traversal Vulnerability
* **Rule Logic:** Inspects target port 80 traffic for raw string values containing relative escape sequence directories (`../`).
* **Use Case:** Identifies exploit payloads targeting web applications to breach localized operational folders.

---

## Live Attack Validation Logging

When active evaluation is run using `snort -A console -q -c snort.rules`, security alerts log directly onto your command terminal dashboard as incidents occur:

```text
06/26-11:50:02.145021 [**] [1:1000001:1] [ALERT] ICMP Ping Sweep/Scan Detected [**] {ICMP} 192.168.1.45 -> 192.168.1.10
06/26-11:51:15.821304 [**] [1:1000002:1] [ALERT] Potential TCP Port Scan Detected [**] {TCP} 192.168.1.45:49152 -> 192.168.1.10:80
06/26-11:53:44.029813 [**] [1:1000003:1] [ALERT] Web Vulnerability Scan Attempt (../) [**] {TCP} 203.0.113.5:58210 -> 192.168.1.10:80
