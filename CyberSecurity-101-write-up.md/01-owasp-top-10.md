# TryHackMe: Cyber Security 101 - OWASP Top 10

## Overview

Cyber Security 101 is TryHackMe's introductory path covering the fu 11 breadth of the field rather than one specialty. It's broken into modules that build on each other:

- **Cyber Security Fundamentals** - networking basics, the CIA triad, common attack types, and how security teams are structured
- **Offensive Security Tooling** - enumeration and exploitation tooling (Nmap, Metasploit, Burp Suite, web app attacks)
- **Defensive Security** - SOC operations, digital forensics, and incident response fundamentals
- **Defensive Security Tooling** - CyberChef, CAPA, REMnux, and FlareVM for analysis and reverse engineering
- **Cryptography** - symmetric/asymmetric encryption and hashing, and where each shows up in real systems

Working through the whole path end to end gave me a working vocabulary and hands-on reps across both the "break it" and "defend it" sides of security - which is exactly the balance I wanted before specializing further.

The room 1 found most demanding, and the one most worth writing up in detail, was **OWASP Top 10**, under the Offensive Security Tooling module.

## OWASP Top 10 Room

This room walks through the ten most critical web application security risks as defined by the OWASP Foundation, with a hands-on vulnerable web app for each category:

1. Injection
2. Broken Authentication
3. Sensitive Data Exposure
4. XML External Entity (XXE)
5. Broken Access Control
6. Security Misconfiguration
7. Cross-Site Scripting (XSS)
8. Insecure Deserialization
9. Components with Known Vulnerabilities
10. Insufficient Logging & Monitoring

Most of the categories clicked quickly - command injection and broken access control, for example, are fairly intuitive once you under stand that the app is trusting input it shouldn't. The two that actually slowed me down were **XXE** and **Insecure Deserialization**, because both require understanding *how the application processes data behind the scenes* before you can see where to attack it. Below is how I worked through each.

