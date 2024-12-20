---
title: Backing Up The System Drive
parent: Backing Up OMV
nav_order: 1
posted: 2024-12-16
updated: 2024-12-17
# looks good 12/17/24
---

{: .note}
UNDER CONSTRUCTION

# Operating System Backup

I choose to keep a backup of my system drive. I installed OMV on a USB drive making it super simple to pop in a new drive and be back up and running if something goes sideways with my installation. I did this for several reasons. First I want my NAS to be as reliable as possible. If I'm storing important data there, I need to make sure I can always access it. I wanted protection from a corrupt drive, bad update, or just me mucking something up.

Since the installation is on a USB drive. I can just shutdown my NAS, pull the drive and clone it on my workstation. This is great, except it means downtime during the clone process. Enter the `openmediavault-backup` plugin.

### openmediavault-backup Plugin

Another wonderful plugin we can install from the `omv-extras` package. Once the plugin is installed, we can navigate to `System > Backup`. This plugin backs up our system drive. It offers multiple options from dd and rsync to fsarchiver and borgbackup along with scheduling. All the documentation can be found here (). I'm going to talk about using `dd full disk` to create an entire OS image.

## My OS Backup Strategy

Here is a link to a post on the [OMV Forums](https://forum.openmediavault.org/index.php?thread/43774-how-to-restore-omv-system-backup-made-with-openmediavault-backup-plugin/) about backing up and restoring using this plugin. Now lets talk about my strategy. I manually run a `dd full disk` backup of my OS after the initial system configuration. I'll also re run a backup after making large non breaking changes (ie adding multiple users or shares). I also run the backup before major update or possible breaking config changes. I only keep my most recent backup and its saved to my RAID0 app storage array. However, this array is also backed up to my RAIDZ2 data array, and again off site.

My OS is on a 64GB USB stick and running the backup takes just shy of an hour.

{: .tip }
A 32GB stick would be ideal and faster, I just didn't have any when I built this system.

Once the backup is complete, I flash the backup image to a second 64GB USB stick. I'll power down my system and swap in the new USB stick. Assuming everything boots I'll do a quick sanity check to make sure I can still access shares and everything looks good. If that is the case, I leave the "fresh" USB stick in my system as the production OS and my original stick gets set aside as my spare. This ensures I have a tested and working backup. The cycle then repeats each time I make a major change.

Now we know what I do. Lets talk about how.


## Running an OS Backup

From `System > Backup > Settings` its as simple as choosing a destination for the backup, a backup method and clicking the `Backup` button. Make sure to `Save` any settings first. We can also set a backup schedule along with number of backups to keep in order to automate the process. I currently do not automate my backups. I just manually run this process before any major changes with the possibly of downtime/breakage or after a large non breaking config change.

I feel comfortable doing this since I put the backup directly into production, save the old system drive, and have this spare image stored in multiple places.

## Restoring the Backup

The `dd full disk` command generates several files. We're interested in the `*.ddfull.zst` file. This contains the entire system image. I use [USBImager](https://bztsrc.gitlab.io/usbimager/) to flash this image. It's oft recommended in the forums and it can flash zst files, unlike BalenaEtcher.

{: .note }
The backup drive needs to be of identical size of the orignial in order for this method to work.

{: .tip}
On my Intel Mac, I needed to manually extract USBImager to my `Applications` folder and launch it from the CLI using `sudo /Applications/USBImager.app/Contents/MacOS/usbimager` to avoid errors.

I usually just mount my OS Backups folder and flash the file from the NAS, via my workstation, to USB. It takes about an hour. I may be able to speed up the process by copying the file to my workstation first but I haven't tried.

Once the image is flashed, I'll shutdown my NAS, unplug the old USB system drive and plug this new one in. I'll monitor the terminal as my NAS boots. It should come up with the familiar GRUB menu followed by the terminal login displaying the correct, read previous, IP address. If this all checks out, I move back to my workstation and make sure I can mount any shares. This is followed by a quick GUI log in to make sure everything is on and where I left it.

## Post Restore

I now have two identical and working copies of my system USB drive. From here, I store the original in a safe place to be retrieved in case of failure or for the next backup cycle. I can now make any updates, upgrades, or possible breaking changes with limited downtime. Rolling back is a simple as shutting down the NAS and swapping USB drives.

## Thoughts and Reasoning

I like this method for several reasons. One I do not need to shut the system down in order to clone the drive. I always have two working copies of the OS, one in production and one that was confirmed good by previously being in production. I also have the most recent backup images stored in several locations. If something goes really sideways, I can remount one of these RAID arrays to pull the image even pull it back from my off site backup. 


