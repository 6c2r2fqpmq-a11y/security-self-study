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

### Capture FIlters & Advanced Filitering
- Applied **capture filiters** (filtering at the point of capture, not just after) and completed **"Filter DNS Communications"** and **"Uncover Suspicious DNS Queries"** - isolating and analyzing DNS traffic to identify potential  indicators of cromprosie.
- Completed **"Find Exposeed Login CRedentials"** - using filiters to locate cleartext credentials transmitted over unecrypted protocols (a common real-world find in network security assessments).

### Coloring Rules & Traffic Classification
- Created custom **coloring rules** in Wireshark to visually distincgusish traffic types, and built an **"HTTPS Traffic DEtector"** challenge to classify encrypted vs. uncrypted traffic at glance.

### TCP Stream Analysis & Evidence Extraction
- Used **"Follow TCP Stream"** to reconstruct full conversations between two hosts from indivual packets.
- Completed **"Extract Web Traffic Evidenc"** and **"Export Suspicious Network Evidence"** - exporting specific packets/streams as evidence, the same workflow used when documents findsings for an incoident report.

### IPv6 & Tshark (Command-Line Analysis)
- Analyzed IPv6 traffic and tracked IPv6 specific traffic patterns.
- Used **Tshark** (Wireshark's command-line counterpart) for traffic analysis - useful for analyzing captures on systems without a GUI, such as servers.




