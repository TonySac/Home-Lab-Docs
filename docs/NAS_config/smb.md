---
title: Samba Shares
parent: OMV Shares 
nav_order: 1
posted: 2024-12-12
#in progress
---

{: .note}
UNDER CONSTRUCTION

# Samba Shares

<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

SMB or Samba is a protocol that allows for easy file sharing accross the network. Lets share one of the newly created folders over the network. First, make sure you've [created a user and group](/docs/NAS_config/users.html) to access this share. The admin and root users are not only restricted from accessing SMB shares, but it's poor security practice to use them for this purpose.

<img src='/assets/NAS/omv/smb_share_wizard.png' width='300'/>{: .float-right}{: .ml-3}

Navigate to `Services > SMB/CIFS`. The SMB service needs to be enabled in the `Settings` pane otherwise we wont be able to connect. Once its enabled, click `Shares` followed by the plus icon to create a share. From this wizard, we can enable sharing, select the shared folder to advertise, add comments, and select some security parameters. Once the share is created, it will show up in the GUI.

## Accessing SMB Share (MacOS)

To access a SMB share on a MacOS workstation use the Finder menu bar following `Finder > Go > Connect to Server...`. Enter the path to the SMB share in the format `smb://ip.of.omv/relative_path_of_share`. You should already know the IP address of the OMV server. The `relative_path_of_share` is found in OMV under the `Storage > Shared Folders` tab and listed next to the share we're trying to access. If done properly, you'll be asked to enter credentials and the share will mount.

### Mount SMB Share on Boot