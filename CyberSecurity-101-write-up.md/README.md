# TryHackMe: Cyber Security 101

A hands-on writeup of my progress through TryHackMe's **Cyber Security 101** learning path. A foundational path spanning offensive security, defensive security, security tooling, and cryptography. This repo documents the modules I found most technically demanding, along with the concepts, tools, and skills I picked across the full path.

## Why this path

I completed Cyber Security 101 to build a broad, hands-on foundation across both the offensive and defensive sides of security before specializing further. This kind of well-rounded bases I think is genuinely useful going into learning entry level cybersecurity. Rather than write up every single room, this writeup  highlights the modules and rooms that pushed me the hardest and taught me the most.

## Modules in this folder

| # | Module | Focus | Writeup |
|---|--------|-------|---------|
| 1 | Offensive Security Tooling - OWASP Top 10 | Web application vulnerabilities: injection, XXE, insecure deserialization, broken access control, and more | [OWASP Top 10](./01-owasp-top-10.md) |
| 2 | Defensive Security Tooling | CyberChef, CAPA, REMnux, FlareVM: malware and forensic analysis tooling | [Defensive Security Tooling](./02-defensive-security-tooling.md) |
| 3 | Defensive Security | SOC structure, digital forensics, incident response | ['03-defensive-security.md'](./03-defensive-security.md) |
| 4 | Cryptography | Symmetric/asymmetric encryption, hashing, John the Ripper, GPG | ['04-cryptography.md'](./04-cryptography.md) |

Each writeup covers the concepts taught, the tools and commands I used, and in some cases tripped me up and how I worked through it.

## Skills & Tools Summary

### Web application security
Identified and exploited OWASP Top 10 vulnerability classes (command injection, XXE, insecure deserialization, broken access control, XSS) against live vulnerable applications. 

### Digital forensics & incident response
Extracted hidden metadata from documents and images ('pdfinfo', 'exiftool') as part of a simulated investigation. Learned the SOC escalation model (L1 → L2 → CIRT) and the incident response lifecycle from detection through lessons learned.

### Malware & static/dynamic analysis
Used CAPA for rapid capability triage of executables, REMnux to deobfuscate and analyze a malicious Office macro end-to-end ('oledump.py', VBA decompression, safe detonation via INetSim), and FlareVM to understand the broader Windows native analysis toolkit.

### Cryptography
Distinguished encoding from encryption, worked with symmetric (AES) and asymmetric (RSA, GPG/PGP) encryption, cracked hashes and passphrase protected keys with John the Ripper ('ssh2john', 'rockyou.txt'), understood hashing's role in integrity verification and HMAC's role in authenticity.

### General tooling
CyberChef (data transformation/decoding), Burp Suite style request manipulation, Linux command line, basic scripting for exploit payload generation (Python).
