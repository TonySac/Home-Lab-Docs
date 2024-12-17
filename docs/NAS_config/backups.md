---
title: Backing Up OMV
parent: NAS Config
nav_order: 99
posted: 2024-12-16
---

{: .note}
UNDER CONSTRUCTION

# RAID is Not A Backup

Okay I've got that out of the way. We already talked about setting up some drives in RAID. RAID gives redudencay, well not in the case of RAID0, but regardless, it is not a backup. In general, RAID protects against drive failure but not data loss. We still need to backup data ideally following the 3-2-1 rule. 3 copies of data on 2 different medias with 1 off site.

Here I'll discuss some of the backup strategies I use, how I've implemented them, and why they work for me.