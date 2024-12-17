---
title: OMV Users & Groups
parent: NAS Config
nav_order: 3
posted: 2024-12-12
# Looks good
---

# OMV Users & Groups
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

# Users

<img src='/assets/NAS/omv/user_anthony.png' width='300'/>{: .float-right}{: .ml-3}

Lets take a minute to talk about users in OpenMediaVault. Users are the people who can either log into the GUI, command line, and/or access shared folders. By default, OMV has a root user and and admin user. We talked a bit about securing access to these users during the [initial setup](/docs/NAS_config/omv.html#host-security).

Navigating to `Users > Users` will show the active users in the OMV system, minus the root and admin accounts. To create a new user, simply click "create" (the plus icon) to open the wizard. Here we can set a new users name, password, groups, and shell permissions. For example, I will add myself as a user without shell access and as a part of the "users" group. Vary these settings in accordance with the user's requirements.

These user credientals will be used to access OMV via the GUI if enabled but more importantly for accessing network shares.

# Groups

By default, all users will be assigned to the group "users". We can also use the groups feature in conjunction with access control lists (ACLs) later down the line to restrict access to shares. Under `Users > Groups` we can modify these settings. For example, I have created a group (anthony) for myself that only contains my user (anthony). 

<img src='/assets/NAS/omv/groups.png'/>

I've also created a family group that contains myself and the other members of my household and use an additional groups for application users. 
