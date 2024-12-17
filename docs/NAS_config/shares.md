---
title: OMV Shares
parent: NAS Config
nav_order: 4
posted: 2024-12-12
#looks good 12/12/24
---

# OMV Shares
{: .no_toc}

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
---

# Defining Shared Folders

Once the [file systems are defined in OMV](/docs/NAS_config/file_systems.html), we can further drill down and create folders in those file systems to share. These basically allow the file system to be seen, "shared", with the OpenMediaVault host. Start by navigating to `Storage > Shared Folders` and clicking the plus icon to create a shared folder. 

<img src='/assets/NAS/omv/share_folders.png' width='300'/>{: .float-right}{: .ml-3}

From here, we can name the share, I'm going to call mine "Anthonys_Cloud", then select a file system from the drop down. I'll be using my data array for this storage folder. By default, the `Relative path` field will be populated with the name but it can be changed if desired. Finally, select the permissions. The permissions range from admin only rights to everyone, even guests, having access. Since this share is for my personal files, I selected the option for admin & users to have read/write access with no access for anyone else.

Upon creation of the folder, it will be listed in the `Shared Folders` menu along with information on its location/path.

<img src='/assets/NAS/omv/share_folder_path.png'/>

## Access Control

We can limit access to individual shares using the permissions or access control lists (ACLs). Selecting a share and clicking "Access control list", denoted by the check box and lines icon, opens the ACL settings. The top section corresponds to standard Linux permissions and should echo what was set when creating this share. Keeping with the previous example, we have admin/root read/write permissions, user group read/write permissions, and no access for anyone else.

<img src='/assets/NAS/omv/new_share_permissions.png'/>

Notice the owner of the share is root. Since the shared folder must be created accessible by root/admin, this will always be the case. Limiting access to other users on the network is best done via group assignment. Other more advanced options are possible but this should cover 99% of home use cases. 

I've already [created a user and group](/docs/NAS_config/users.html) for myself. By setting the group permissions, I am limiting access to this shared folder to the root/admin user and members of the defined group. The "Replace" and "Recursive" boxes must also be checked. 

<img src='/assets/NAS/omv/limit_share_group.png'/>

Once the share is defined on the host with proper permissions, it can shared on the network using one of the file sharing protocols in OMV.
