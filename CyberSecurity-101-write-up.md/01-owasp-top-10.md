# TryHackMe: Cyber Security 101 - OWASP Top 10

## Overview

Cyber Security 101 is TryHackMe's introductory path covering the fu 11 breadth of the field rather than one specialty. It's broken into modules that build on each other:

- **Cyber Security Fundamentals** - networking basics, the CIA triad, common attack types, and how security teams are structured
- **Offensive Security Tooling** - enumeration and exploitation tooling (Nmap, Metasploit, Burp Suite, web app attacks)
- **Defensive Security** - SOC operations, digital forensics, and incident response fundamentals
- **Defensive Security Tooling** - CyberChef, CAPA, REMnux, and FlareVM for analysis and reverse engineering
- **Cryptography** - symmetric/asymmetric encryption and hashing, and where each shows up in real systems

Working through the whole path end to end gave me a working vocabulary and hands-on reps across both the "break it" and "defend it" sides of security - which is exactly the balance I wanted before specializing further.

The room I found most demanding, and the one most worth writing up in detail, was **OWASP Top 10**, under the Offensive Security Tooling module.

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

Most of the categories clicked quickly - command injection and brok en access control, for example, are fairly intuitive once you under stand that the app is trusting input it shouldn't. The two that act ually slowed me down were **E** and **Insecure Deserialization**, because both require understanding *how the application processes d ata behind the scenes* before you can see where to attack it. Below is how I worked through each.

### Deep Dive: XML External Entity (XXE)
**The concept:** XML documents can define custom "entities" inside a DOCTYPE declaration - essentially variables that get substituted into the document when it's parsed. If an XML parser is configured to resolve *external* entities (ones pointing to a file path or URL rather than a literal string) and it's parsing user-supplied XML, an attacker can define an entity that points at a file on the server's filesystem. When the parser resolves it, the file's contents get echoed back into the application's output.

This was the first room in the path where I had to actually understand a file format's spec (not just guess at a syntax) before I could exploit anything. I had to get comfortable with DTDs (Document Type Definitions): what defines a valid XML structure before the entity substitution trick made sense.

**What I did:**

First, I confirmed the injection point was actually parsing my DTD by sending a harmless custom entity and checking that it rendered in the response:


<}xmI version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [
 <!ELEMENT foo ANY >
 <!ENTITY xxe "test value" >
]>
<foo>&xxe; </ foo>

Once that confirmed the app would substitute my entity, I swapped the entity's value from a literal string to a 'SYSTEM' identifier pointing at a local file:

<?xm] version="1.0" encoding="ISO-8859-1"?>
< IDOCTYPE foo [
 <!ELEMENT foo ANY >
 <!ENTITY xxe SYSTEM "file:///etc/passwd" >
]>
<foo>&xxe; </foo>


The server dutifully read the file and returned its contents in the page response - which is the core of the vulnerability. From there I used the same technique against /home/<user≥/. ssh/id_rsa to pul 1 a private SSH key straight off the box, which drove home just how much damage an "it just reads a file" bug can actually do - arbitra ry file read this way can lead directly to full account/system comp romise if credentials or keys are exposed.


