# TryHackMe: Defensive Security

## Overview

This module builds the foundation for the "blue team" side of securi ty: how a Security Operations Cent er (SOC) is structured, how digita 1 forensics investigations work, a nd how incident response actually gets carried out once something go es wrong. It's the conceptual coun terweight to the offensive modules
instead of asking "how do I brea k in," it asks "how do I know some thing broke in, and what do I do a bout it."

## Topics & Rooms Covered

- Introduction to Defensive Securi ty (SOC structure, digital forensi cs fundamentals, incident response basics)
- Digital Forensics case work (fil e/metadata analysis)
- Incident response fundamentals
## Security Operations Center (SO
C) Fundamentals
A SOC is the team responsible for continuously monitoring an organiz ation's environment and responding
when something looks wrong. This r oom laid out how a SOC is typicall
y staffed and how work escalates:
- **L1 Analysts** - the front lin e, triaging incoming alerts and de ciding what's noise vs. what needs escalation
- **L2 Analysts** - handle the mor e complex cases L1 passes up, doin
- e complex cases L1 passes up, doin g deeper investigation
- **Engineers** - own and tune the tools (SIEM, EDR) the rest of the team depends on
- **CIRT/CSIRT/CERT** - the "firef ighters" called in when an inciden t is confirmed and needs full inci dent response, not just alert tria ge
Understanding this hierarchy matte red more than I expected - a lot o f the practical rooms in this path (and the OWASP room) simulate what an L1/L2 analyst would actually be staring at: a single suspicious fi le, log, or session, and the job i s to figure out if it's actually a threat before it goes any further up the chain.
## Digital Forensics: File & Metad ata Analysis

The hands-on forensics exercise in this module was a mini investigati on: given a case file (a PDF and a n attached image), the goal was to extract hidden information from me tadata rather than the visible con tent of the files.
**Tools used:**
- **'
pdfinfo'** (from 'poppler-uti
1s') - reads a PDF's embedded meta data: author, creation tool, subje ct, and timestamps. This alone can reveal who actually created a docu ment, even if the visible content gives no clue.
- **'exiftool'** - reads (and can write) metadata across many file t ypes, most usefully image EXIF dat
a. In this case, an image attached to the document still had its embe
dded GPS coordinates intact, which pinpointed the location it was tak

en - information the sender clearl
y didn't intend to hand over.
The lesson that stuck with me: att ackers (and in this case, the fict ional "kidnappers" scenario the ro om built around) routinely leak fa r more than they mean to through m etadata alone. A big part of digit al forensics isn't exotic tooling
- it's knowing to check the borin g, easy-to-overlook fields every f ile carries by default.
## Incident Response Fundamentals
This portion covered the lifecycle an organization follows once an in cident is confirmed - generally:
**preparation → identification → c ontainment → eradication → recover y → lessons learned**. The main po int the room drove home is that re sponding to an incident isn't iust
en - information the sender clearl
y didn't intend to hand over.
The lesson that stuck with me: att ackers (and in this case, the fict ional "kidnappers" scenario the ro om built around) routinely leak fa r more than they mean to through m etadata alone. A big part of digit al forensics isn't exotic tooling
- it's knowing to check the borin g, easy-to-overlook fields every f ile carries by default.
## Incident Response Fundamentals
This portion covered the lifecycle an organization follows once an in cident is confirmed - generally:
**preparation → identification → c ontainment → eradication → recover y → lessons learned**. The main po int the room drove home is that re sponding to an incident isn't iust
set s the organization up to be hit th
e same way again.
## Takeaways

This module gave me the operationa 1 picture that the more technical rooms (like OWASP Top 10, or the t ooling module) sit inside. Knowing
*how* to exploit or analyze someth ing matters, but this module is wh at connects that skill to an actua
1 job function: who looks at the a lert first, what they check, and h ow a confirmed incident gets handl ed from detection to lessons-learn ed. It's also where I first practi ced the instinct of "check the met adata before you assume you only h ave what's on the surface" - a hab
it that showed up again later in t he more technical rooms.
