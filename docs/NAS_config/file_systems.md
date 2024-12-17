---
title: OMV File Systems
parent: NAS Config
nav_order: 2
posted: 2024-12-09
updated: 2024-12-11
#looks good 12/11
---

# OMV File Systems
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

# Can I See The Drives?

Before we can even setup a file system, our machine needs to be able to see the drives. Assuming all of the drives have been installed in the machine, they should be visible under `Storage > Disks`. 

<img src='/assets/NAS/omv/drives.png'/>

Ideally, file systems should be defined on clean drives. I started this build with fresh hard drives but still performed a quick wipe on them prior to writing the file system. Now is a good time to wipe all the disks.

{: .warning}
This will erase any data currently on the drive. Make sure you select the correct disk!

Navigate to `Storage > Disks` and select the drives to be wiped. Click the eraser icon then follow the on screen prompts to wipe the drive.

<img src='/assets/NAS/omv/wipe_drive.png'/>

# Configuring the File Systems

I settled on using ZFS for my data array's file system. It seems to be the current standard for data storage and security. I was between ZFS and BTRFS simply because BTRFS appeared to be natively supported by OMV. I'm also using standard software RAID for my application storage drives.

{: .info}
A lot of ZFS info was borrowed from [raulfg3's post](https://forum.openmediavault.org/index.php?thread/7633-howto-instal-zfs-plugin-use-zfs-on-omv/) on the OMV forums and adapted for my current version of OMV.

## Installing the PVE Kernel

{: .note }
This plugin is found in the `omv-extras` package which was installed during [my initial deployment of OMV](/docs/NAS_config/omv.html#omv-extras).

<img src='/assets/NAS/omv/install_kernel.png' width='300'/>{: .float-right}{: .ml-3}

The Proxmox kernel is required to run ZFS. Start by finding and installing `openmediavault-kernel` plugin. Once it installs, navigate to the new tab under `System > Kernel`. On the top toolbar, highlight the icon that looks like a download box and install the Proxmox kernel. I selected the most recent (kernel 6.11 as of this document). The install will take some time. Once it completes, the new kernel should automatically have been selected as the default. 

Reboot the system.

Once the system reboots, make sure it booted with the new kernel. Under `Diagnostics > System Information` the kernel field should display the newly applied kernel.

<img src='/assets/NAS/omv/kernel_version.png'/>

{: .tip}
The PVE Kernel is required before installing the ZFS plugin. I don't think it matters too much in regards to other parts of the system but I figured it was best to be installed first. This avoids an almost complete configuration breaking due to a kernel change.

# Multiple Disk and Device Management (mdadm) RAID

<img src='/assets/NAS/omv/md_tab.png' width='300'/>{: .float-right}{: .ml-3}

Install the `openmediavault-md` plugin. We should be pretty good at this by now so I don't think I need to tell you where to go. Once it installs, the `Multiple Device` tab should be visible in the `Storage` menu.

From here, we can create a multiple device, commonly known at RAID, software array. Select the RAID level and devices followed by `Save`. In this example I used the stripe level. This does not provide any redundancy. In fact, it sometimes can be considered less reliable because if one disk fails all data is lost.

The array should now be displayed as a device in the GUI along with related information.

<img src='/assets/NAS/omv/md_array.png'/>

## Create and Mount the File System

<img src='/assets/NAS/omv/create_file_sys.png' width='300'/>{: .float-right}{: .ml-3}

We now need to create a file system on this array and mount it to OMV. Navigate to `Storage > File Systems` and click the plus icon labeled "Create abd mount a file system." From here we can choose from a basic EXT4 system all the way to BTRFS. Make sure to pick the system appropriate for your use case. In this example I'm using the array for application storage, particularly Docker, so EXT4 is ideal.

The next page asks for device selection. The previously created array should be visible in the dropdown as an `mdX` device along with any other disks installed on the system. The individual drives that make up `mdX` should not be visible. The following step will ask you to select the file system to be mounted along with a usage alert. Upon completing these steps, the new file system should be mounted in OMV and visible in the file system tab of the GUI.

<img src='/assets/NAS/omv/file_sys_gui.png'/>

# ZFS

{: .tip }
ZFS requires the system be booted with the [PVE kernel](/docs/NAS_config/file_systems.html#installing-the-pve-kernel) prior to installing any ZFS plugins or configuration.

<img src='/assets/NAS/omv/zfs_tab.png' width='200'/>{: .float-right}{: .ml-3}

Find the ZFS plugin under `System > Plugins > openmediavault-zfs`. 

Once it is installed, the navigation bar should have a new `zfs` tab under `Storage`. Make sure any drives destined for the ZFS pool have been wiped prior to proceeding.

## Creating the ZFS Pool

<img src='/assets/NAS/omv/zfs_pool_options.png' width='300'/>{: .float-right}{: .ml-3}

With clean drives, we can build our ZFS pool. Navigate to that new `zfs` tab and select `Pools` followed by the plus icon to add a pool. This opens the pool creation menu.

Give the pool a name. I chose the name `data` as this pool will be used for data storage. I'm sure there are some best practices here but I just winged it. Select the pool type and devices for the pool. In this example I'm using all 4x of my 2TB spinning drives in a RAIDZ2 configuration. This gives me 4TB of usable storage with the ability to sustain 2 disk failures. I kept the remaining options with their default assignments.

The pool will be created and visible from the the GUI. As seen here I have a 3.41TB pool which makes sense as I used 4x 2TB drives in a RAIDZ2 configuration.

<img src='/assets/NAS/omv/zfs_pool_details.png'/>

## ZFS File System

After creating the ZFS pool, it will automatically appear as a listed file system in the OMV GUI. No other configurations needed.

<img src='/assets/NAS/omv/post_zfs_file_sys.png'/>


# Final Thoughts

Setting up the RAID array and ZFS file system, along with mounting them is pretty straight forward in the GUI. The biggest challenge is realizing that plugins are needed for these setups along with the PVE kernel for ZFS.

I outlined these steps using examples from my setup but they can be repeated and varied depending on the use case.
