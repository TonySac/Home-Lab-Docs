---
title: Docker on OMV
parent: NAS Config
nav_order: 5
posted: 2024-12-09
updated: 2024-12-12
#Looks good 12/12/24
---

{: .info}
I borrowed a lot of this information from the [Docker in OMV 7](https://wiki.omv-extras.org/doku.php?id=omv7:docker_in_omv) guide on [omv-extras.org](https://wiki.omv-extras.org/)


# Running Docker on OMV
{: .no_toc}

<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

{: .note }
Docker requires the `omv-extras` package which was installed during [my initial deployment of OMV](/docs/NAS_config/omv.html#omv-extras).

Part of the reason I chose OMV as my NAS OS was due to the Docker support. I plan on at least running [Frigate](https://frigate.video) and maybe a few other containers on this system. To get started, enable the "Docker repo" under the `System > omv-extras` tab. Once that is done, the `openmediavault-compose` plugin can be installed.

We also need a few [shared folders](/docs/NAS_config/shares.html#defining-shared-folders) for Docker to function. At minimum we need a folder for persistent app data, backups, and docker image storage. They can be named using whatever scheme you prefer. They should also be located on a separate drive from the OMV system. I used that NVMe RAID0 array I set up earlier with the following structure:

<img src='/assets/NAS/omv/docker_folders.png' width='400'/>{: .float-right}{: .ml-3}

* /md0
    - /docker
        - /appdata
        - /backup_compose
        - /docker

# Compose Settings

Navigate to `Services > Compose > Settings`. In this area we will tell the compose plugin where to find and write files using the shares we just setup. 

<img src='/assets/NAS/omv/compose_settings.png' width='400'/>{: .float-right}{: .ml-3}

**Compose Files** - This is where the obvious, compose files, are stored, along with persistent container data. The drop down menu should be populated with the available shares. 

**Data** - This path acts like a variable for use in the Docker Compose files. For now, I'm ignoring it as I will specify data locations per container. 

**Backup** -  A backup location for persistent data. Once again, the drop down should populate with available shares. I'm keeping it on the same NVMe array as I'll only use it to restore a broken container and this whole array will be backed up. 

**Docker** - Docker stores images and system data here.. This path needs to be manually inputted from the absolute path of the share.



# Check the Config

So we've got the plugin installed and all of the paths set. Normally, Docker has us run the `hello-world` container in the CLI to conifrm everything is working. The OMV plug in only runs off Docker Compose and unless we're in the CLI, everything is done via the GUI. Fortunately, I came across this [cccheck/hello-world](https://hub.docker.com/r/crccheck/hello-world/) image that spins up a container serving a simple http website.

I've adopted the run command as a compose file on port 8000:

```docker
services:
    hello-world:
        image: crccheck/hello-world
        container_name: hello-world
        ports:
            - 8000:8000
```

<img src='/assets/NAS/omv/ascii.png' width='300'/>{: .float-right}{: .ml-3}

Add a new compose file under `Services > Compose > Files` by clicking the plus icon and pasting in the above compose example. Start the container. If it successfully starts, we should also be able to navigate to `host.ip:8000` and see a website with an ASCII Docker logo.

# Next Steps

Now that Docker is running, we can get started on setting up some real containers! I've included some documentation on the containers I'm running and how I set them up.