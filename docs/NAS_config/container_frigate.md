---
title: Frigate
parent: Docker on OMV
nav_order: 1
posted: 2024-12-20
# in progress
---

{: .note}
UNDER CONSTRUCTION

# Frigate NVR

[Frigate](https://frigate.video) is an open source, self hosted, network video recorder. I've been using it for several years with my home security cameras along with [Home Assistant](https://www.home-assistant.io). I originally ran Frigate in a Docker container alongside my other services. When I converted to ProxMox I quickly spun up Frigate in an LXC using one of the [TTeck Proxmox Helper Scripts](https://tteck.github.io/Proxmox/). RIP. Then for the sake of my own learning/tourture, I built and configured my own LXC to run Frigate.

I've decided to run return to the supported Docker configuration of Frigate for stability and run it on this NAS for a possible performance boost.

## Frigate Directories



## Frigate Compose File

{: .warning }
The Frigate container does not support the PUID or PGID variables and must run as root. For this reason, I did not set an "appuser" as outlined in the omv-extras documentation. Consider the security implications this may have on your system.

The Frigate docs include an example [compose file](https://docs.frigate.video/frigate/installation#docker) to get started. I've been running Frigate for awhile so I already have one that works great for me. I've included a sanitized copy of it here with some comments.

```yaml
services:
  frigate:
    container_name: frigate
    restart: unless-stopped # Removed privileged flag
    image: ghcr.io/blakeblackshear/frigate:stable
    shm_size: "64mb" # Default size, re evaluated with formula if more cams added
    devices:
      - /dev/bus/usb:/dev/bus/usb # Passes the USB Coral
      - /dev/dri/renderD128:/dev/dri/renderD128 # Passes Intel GPU
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - ./config:/config # Bind mount for config. Uses appdata folder on OMV
      - /data/frigate:/media/frigate # Bind mount for footage. Uses share on OMV NAS
      - type: tmpfs # Optional: 1GB of memory, reduces SSD/SD Card wear
        target: /tmp/cache # Left default, may need to be evaluated for location
        tmpfs:
          size: 1000000000
    ports:
      - "8971:8971"
      - "5000:5000" # Internal unauthenticated access. Expose carefully. (Enabled/disabled as needed for trouble shooting)
      - "8554:8554" # RTSP feeds
      - "8555:8555/tcp" # WebRTC over tcp
      - "8555:8555/udp" # WebRTC over udp
      - "1984:1984" # Go2Rtc
    environment: # Removed  LIBVA_DRIVER_NAME: "radeonsi" env var. Previous GPU was AMD.
      FRIGATE_RTSP_PASSWORD: "password" # Using real password, this is the sanitized version
    cap_add: # Needed for GPU/performance monitoring with unprivileged container
      - CAP_PERFMON
```


<!-- NOTES  

cap mon perf event 2 -->