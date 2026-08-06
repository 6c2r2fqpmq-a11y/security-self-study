# TryHackMe: Defensive Security

## Overview

This module builds the foundation for the "blue team" side of security: how a Security Operations Center (SOC) is structured, how digital forensics investigations work, and how incident response actually gets carried out once something goes wrong. It's the conceptual counterweight to the offensive modules. Instead of asking "how do I break in," it asks "how do I know some thing broke in, and what do I do about it."

## Topics & Rooms Covered

- Introduction to Defensive Security (SOC structure, digital forensics fundamentals, incident response basics)
- Digital Forensics case work (file/metadata analysis)
- Incident response fundamentals

## Security Operations Center (SOC) Fundamentals

A SOC is the team responsible for continuously monitoring an organization's environment and responding when something looks wrong. This room laid out how a SOC is typically staffed and how work escalates:

- **L1 Analysts** - the front line, triaging incoming alerts and deciding what's noise vs. what needs escalation
- **L2 Analysts** - handle the more complex cases L1 passes up, doing deeper investigation
- **Engineers** - own and tune the tools (SIEM, EDR) the rest of the team depends on
- **CIRT/CSIRT/CERT** - the "firefighters" called in when an incident is confirmed and needs full incident response, not just alert triage

Understanding this hierarchy mattered more than I expected. A lot of the practical rooms in this path (and the OWASP room) simulate what an L1/L2 analyst would actually be staring at: a single suspicious file, log, or session, and the job is to figure out if it's actually a threat before it goes any further up the chain.

## Digital Forensics: File & Metadata Analysis

The hands-on forensics exercise in this module was a mini investigation: given a case file (a PDF and an attached image), the goal was to extract hidden information from metadata rather than the visible con tent of the files.

**Tools used:**

- **'pdfinfo'** (from 'poppler-uti1s'): reads a PDF's embedded meta data: author, creation tool, subject, and timestamps. This alone can reveal who actually created a document, even if the visible content gives no clue.
- **'exiftool'** - reads (and can write) metadata across many file types, most usefully image EXIF data. In this case, an image attached to the document still had its embedded GPS coordinates intact, which pinpointed the location it was taken.

The lesson that stuck with me: attackers (and in this case, the fictional "kidnappers" scenario the room built around) routinely leak far more than they mean to through metadata alone. A big part of digital forensics isn't exotic tooling. It's knowing to check the boring, easy-to-overlook fields every file carries by default.

## Incident Response Fundamentals

This portion covered the lifecycle an organization follows once an incident is confirmed generally:
**preparation → identification → containment → eradication → recovery → lessons learned**. The main point the room drove home is that responding to an incident isn't just a technical exercise. It's a coordinated process with defined roles, communication plans, and follow up documentation, because a technically "solved" incident that isn't documented and learned from just sets the organization up to be hit the same way again.

## Takeaways

This module gave me the operational picture that the more technical rooms (like OWASP Top 10, or the tooling module) sit inside. Knowing *how* to exploit or analyze something matters, but this module is what connects that skill to an actua1 job function: who looks at the alert first, what they check, and how a confirmed incident gets handled from detection to lessons learned. It's also where I first practiced the instinct of "check the metadata before you assume you only have what's on the surface." This was a habit that became useful again later in the more technical rooms.
