---
title: NAS Config
nav_order: 97
posted: 2024-12-09
#looks good 12/9/24
---

# Configuring my NAS
{: .no_toc}

<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Operating System

I went back and forth on the best operating and file systems for my NAS. Ultimately I settled on running [OpenMediaVault](https://www.openmediavault.org). I currently run OMV in a VM. OMV is also based on Debian, my Linux distro of choice, so I'm pretty familiar with the system and whats under the hood. Plus it's light weight and appears to have better Docker compatibility than some alternatives. The OS will be installed on a USB drive for ease of backup and to maximize storage space.

## Storage

Currently, the box is outfitted with 4x 2TB 3.5" spinning disks and 2x 128GB NVMe drives. I also have 2 free SATA ports for expansion (if I can find room in the case). 

As of now the plan is to run the 2x NVMe drives in RAID0 to take advantage of all 256GB. Unfortunately, there will be no redundancy, but these drives are slated to be application storage and will be backed up to my data storage drives.

The 4x 2TB drives will be used as data storage in a RAIDZ2 configuration. Giving me a total of 4TB usable space with redundancy to support 2 drive failures.

## Backups

I plan to backup the operating system prior to major updates/changes. The image will be written to a USB drive and validated. I will likely then swap this new drive into production and keep the old one as a backup. This should prove my backup works and give me the ability to just swap out my USB boot media in the event of a catastrophic failure.

The application storage drives will be backed up to my data array. The data array will be synced with my workstation storage for the time being along with one of my cloud providers (probably iCloud). This pretty much covers the 3-2-1 backup rule Eventually, I plan to place an off site NAS at my parents place for a completely self-hosted solution.

The following pages outline the installation and configuration of my NAS software: