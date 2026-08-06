# TryHackMe: Defensive Security Tooling

## Overview
This module is a hands-on tour of the tools defenders actually reach for once an alert fires or a suspicious file lands on a desk: **CyberChef**, **CAPA**, **REMnux**, and
**FlareVM**. Where the offensive side of the path is about finding a way in, this module is about *what happens after*, how an analyst pulls apart a file, a script, or a network capture to figure out what it does before it does damage.

## Rooms Covered
- CyberChef: The Basics
- CAPA: The Basics
- REMnux: Getting Started
- FlareV: Arsenal of Tools

## CyberChef: The Basics

CyberChef is a browser-based tool for chaining together data transformations: decoding, encoding, hashing, extracting, regexing without writing a script for each one-off task. The core idea is a "recipe": you drag operations onto a canvas (e.g•, 'From Base64" → 'Extract IP Addresses') and CyberChef pipes your input through each stage in order.

What stood out to me: a huge amount of "find the malicious payload" work in incident response is really just repeated decodin: obfusca ted scripts are often layered (base64 inside URL-encoding inside base64 again), and CyberChef lets you stack those transforms visually in stead of writing throwaway Python for each layer. I used the extract or operations (IP addresses, email addresses, domains) to quickly pull indicators of compromise out of a blob of text, which is exactly the kind of task a SOC analyst does dozens of times a day when triaging a phishing email or log dump.

## CAPA: The Basics

CAPA is a static analysis tool that inspects an executable and reports the *capabilities* it finds: things like "can write to the registry, " "can create a scheduled task," "contains code that looks like a keylogger" by matching patterns against a large open rule set, without actually running the file.

The value here is speed: instead of manually reverse engineering a binary from scratch, CAPA gives an analyst a same-day answer to "roughly what does this thing do and how worried should I be," which is often enough to decide whether a sample needs a deeper look from a malware analyst or can be triaged as low 

## REMnux: Getting Started

REMnux is a Linux distribution pre-loaded with malware and forensic analysis tooling. This room had me analyze a malicious Office document ('xIsm') suspected of hiding a macro:

1. Used 'oledump.py' to list the 0LE2 data streams inside the file and identify which stream contained a macro (flagged with an 'M' in the output).
2. Dumped that stream and applied the '--vbadecompress' flag to turn the raw hex into readable VBA source.
3. Read through the decompressed macro to find the actual malicious behavior: in this case, code that downloaded and executed a second-stage payload.
4. Used **INetSim** to simulate network services (DNS, HTTP, etc.) inside an isolated environment, so the malware could be *detonated* safely and its network behavior observed without it reaching anything real.

## FlareVM: Arsenal of Tools

FlareVM is the Windows counterpart to REMnux: a Windows VM pre-loaded with reverse engineering, forensics, and malware analysis tools (disassemblers, PE analyzers, network monitors, etc.), built for analyzing Windows-native malware in an environment that actually resembles what the malware was written to target.

