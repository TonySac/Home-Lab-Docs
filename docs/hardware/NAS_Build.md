---
title: NAS
parent: Hardware
nav_order: 3
posted: 2024-12-05
# in progress with NAS build
---

{: .note}
COMING SOON

# DIY NAS

I've put off setting up a NAS for awhile. Right now I use iCloud for some data storage, along an external drive. I also have/had and external drive taped to my server that acts as a single drive NAS of sorts running off an Open Media Vault VM. All good homelabbers have a NAS so I should too. Plus I want to be able to self host most of my storage, have redundancy, and reliability as I add more services. 

I don't have a lot of media to store other than photos. I'm not a Plex or Jellyfin user so I don't need massive amounts of storage. I do however want a bulletproof solution that won't fail randomly or due to some other tinkering. That leads me to a dedicated NAS device.

# NAS Hardware

I listen to the Slef-Hosted podcast and heard episode __ recently with guest Brian Moses talking about his NAS builds. I expolresd his page and settled on my version of his 2023 Econo NAS.

I chose to build my NAS with the following componets:

* Case
* PSU
* 2x 128 SSD
* 4x 2TB HD
* USB Boot Drive
* MoBo
* RAM

The idea is to run Open Media Vault. I'm already familiar with it and its lightweight plus it supports Docker and KVM. That's important because I'd also like to run Frigate on this box. From there I will likely set up the two SSDs in a RAID0 to store app and Docker data. I'm looking at ZFS with RAIDZ1 or RAIDZ2 for my 2TB HDs. I think 2TB of usable storage will be more than enough for me. I can use 3x drives in RAIDZ1 for 4TB of storage with 1 redundant drive or in RAIDZ2 for 2TB storage and 2 redundant drives. That leaves my 4th drive as Frigate only storage. Or I can use all 4 drives in RAIDZ2 for 4TB storage with 2 redundant drives and store my Friagte footage on the NAS. I can also explore shcucking some of the external drives I have laying around and installing those for Frigate stroage. 
