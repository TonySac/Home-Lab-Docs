---
title: OMV Users & Groups
parent: NAS Config
nav_order: 3
posted: 2024-12-12
updated: 2024-12-20
#Proofed & Good 12/20/24 (Appuser is unused and commented out until needed.)
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

These user credentials will be used to access limits parts of OMV's GUI but more importantly for accessing network shares.

# Groups

By default, all users will be assigned to the group "users". We can also use the groups feature in conjunction with access control lists (ACLs) later down the line to restrict access to shares. Under `Users > Groups` we can modify these settings. For example, I have created a group (anthony) for myself that only contains my user (anthony). I've also created a family group that contains myself and the other members of my household.

<img src='/assets/NAS/omv/groups.png'/>


# Docker/App Users

I pursued the idea of creating an application, "appuser", user for use with Docker. Due to some limitations with the Frigate container, this was not 100% feasible. I plan to revisit this if/when the need arises. In the meantime, more information about an "appuser" account and its importance for security with Docker can be found [here in the omv-extras docs](https://wiki.omv-extras.org/doku.php?id=omv7:docker_in_omv#user_and_permission_management_in_docker_and_omv_more_security).

<!-- In the interst of security we should define at least one user to run applicatons or Docker containers. In this manner, we can limit the amount of access these applications have to our system and files. I chose to create a seperate usesr for each application, further resistricging access.

> EXAMPLE:
> I have a Manyfold container to organize my 3D models. This container only needs to be able to read and write to the share where my models are kept. There is no need for Manyfold to access personal photos or sensitive documents, let alone the root file system, of my NAS. By creating a `manyfold` user with permissions to only access the 3D models, then running my container as that user, I have limited the container's access.

{: .tip }
Users created in the GUI are stuck added to the `users` group with all associated permissions. This must be overriden by creating the user in the CLI.

## Creating an Application User

Let's walk though creating an application user and groud with limited pemissions. This requires us logging into the OMV CLI. I will be using the `manyfold` user as an example.

In the CLI we can add our manynfold user:

```bash
adduser -U manyfold
```

In the GUI we should now see the manyfold user as a member of the manyfold group along with the associated UID and GID.

{IMAGEP}

DONT MOD USER IN GUI WILL ADD TO USERS GROUP.

We now have a user that is lmited in access

permissions key file for shares


Let -->