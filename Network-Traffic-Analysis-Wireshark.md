# Network Traffic Analysis - Wireshark

## Objective
Completed LabEx's "Wireshark for Beginners" course (20 labs/challenges) to build hands on skill in packet capture, filtering, and protocol level traffic analysis, supplemented by additional self study on Wireshark's interface and statistics tools.

## Course
[LabEx - Wireshark for Beginners](https://labex.io/courses/wireshark-for-beginners)

## Supplementary Learning
Watched ['Mastering Wireshark: The Complete Tutorial"](https://www.youtube.com/watch?v=a_4MjV_-75w) (Hacker Joe) to reinforce interface navigation, filtering syntax, coloring rules, and Wireshark's built-in statistics tools (covered in the LabEx labs below, plus TCP/UDP protocol behavior for DHCP and DNS).

## What the Course Covered

### Setup & Interface
- Installed and verified Wireshark, explored and customized the interface, and the configuration column display for faster packet triage.

### Packet Capture & Basic Filtering
- Captured live network traffic and applied **display filters** to isolate specific protocols.
- Completed **"Filter Encrypted Web Traffic"**: identifying and isolating TLS/HTTPS traffic using filter syntax.

> Note: add a specific filte

### Capture FIlters & Advanced Filtering
- Applied **capture filters** (filtering at the point of capture, not just after) and completed **"Filter DNS Communications"** and **"Uncover Suspicious DNS Queries"** - isolating and analyzing DNS traffic to identify potential  indicators of compromise.
- Completed **"Find Exposed Login CRedentials"** - using filters to locate cleartext credentials transmitted over unencrypted protocols (a common real-world find in network security assessments).

### Coloring Rules & Traffic Classification
- Created custom **coloring rules** in Wireshark to visually distinguish traffic types, and built an **"HTTPS Traffic DEtector"** challenge to classify encrypted vs. unencrypted traffic at glance.

### TCP Stream Analysis & Evidence Extraction
- Used **"Follow TCP Stream"** to reconstruct full conversations between two hosts from individual packets.
- Completed **"Extract Web Traffic Evidence"** and **"Export Suspicious Network Evidence"** - exporting specific packets/streams as evidence, the same workflow used when documents findings for an incident report.

### IPv6 & Tshark (Command-Line Analysis)
- Analyzed IPv6 traffic and tracked IPv6 specific traffic patterns.
- Used **Tshark** (Wireshark's command-line counterpart) for traffic analysis - useful for analyzing captures on systems without a GUI, such as servers.

### Why This Matters for Security Work
This directly overlaps with detection work in my [Splunk SIEM lab](https://github.com/6c2r2fqpmq-a11y/home-siem-lab-splunk): both involve filtering large volumes of data down to the specific events that matter (DNS anomalies, suspicious auth traffic) and documenting findings as evidence. The "Find Exposed Login Credentials" and "Uncover Suspicious DNS Queries" challenges in particular mirror real SOC triage work.

## Skills DEmonstrated
- Wireshark display and capture filter syntax
- DNS and TLS/HTTPS traffic analysis
- TCP stream reconstruction and evidence export
- Coloring rules for rapid visual triage
- Command-line packet analysis with Tshark

## Evidence





