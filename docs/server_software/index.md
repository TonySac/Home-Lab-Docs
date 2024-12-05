---
title: Server Software
nav_order: 3
posted: 2024-09-20
---

{: .note}
UNDER CONSTRUCTION - ALL THESE PAGES ARE IN PROGRESS AND SUBJECT TO CHANGE AS I WORK THROUGH A REBUILD.

# Server Software

I initially started with base Debian system and Docker. Although this worked fine for my use case, it wouldn't be a home lab if I didn't decide to mess around a bit. So I broke things and converted over to Proxmox. The big advantage Proxmox gives me is the ability to spin up new VMs or CTs to dry run apps without affecting my production system. Once I've configured and vetted them, I'm good to go live or replace the old ones. Although I still manage to screw that up sometimes.