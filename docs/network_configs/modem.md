---
title: Modem Config
parent: Network Config
nav_order: 1
posted: 2024-12-05
# NEEDS PICS otherwise ok 12/05/24
---

{: .note}
UNDER CONSTRUCTION - Awaiting images

# Modem

Lets start with my ISP & modem setup. I have a fiber connection that terminates in my house at a Calix 844GE-1 ONT & router combo.

Its a basic enough device but worked fine in the beginning when I used it as a DHCP server. Now that I've upgraded to OPNSense, I needed a way to pass my WAN though to the OPNSense box.

Unfortunately, I cannot find an easy way to place this ONT in bridge mode. I've heard of some users having success calling their ISP and having it done that way. I elected to use the DMZ method. 

Here is how I've setup my ONT. First I'm assuming you have internet, access to the admin GUI, and the OPNSense box is plugged into the ONT.

Under the quick start menu, I set static DNS servers to some of the publicly available ones. I'm using Google's `8.8.8.8` and Cloudflare's `1.1.1.1`. This ensures the ONT should always have DNS resolution & internet access.

I then configured a wireless network SSID and password on the ONT. I set this to only use the 2.4 G radio and disabled broadcasting.  I did this so I always have a wireless backdoor into the ONT admin interface should something go sideways.

Moving onto the advanced settings, I changed the DHCP addressing range. The default is `192.168.1.0/24`. Previoslut I ran into issues with my VPN due to this being a common range. I chose something outside the default ranges to make sure there was no conflicts down the road say `192.168.69.0/24` (nice). This gave the ONT an IP of `192.168.69.1`. I then created a DHCP reservation for the OPNSense box and one for my laptop. The only device that should ever be connected to the ONT is the hardwired OPNSense router, and maybe my laptop. Since they both have DHCP reservations, I can quickly tell if something else was connected.

{: .tip }
I believe I can also narrow the IP addressing range from the ONT admin interface. This can further restrict the devices able to connect to the ONT's network.

Under Security options, I changed the default admin credentials as good practice. Then I enabled and placed the OPNSense router's DHCP reservation in the DMZ.

I also checked a few other security features such as maxing the ONTs firewall settings, disabling UPnP, and disabling remote management.

# Final Thoughts

From what I can tell, this has given me a bit of a double NAT situation but so far has not caused me any major trouble. The ONT only sees devices that are directly connected, so the OPNSense box and maybe my laptop for troubleshooting. All firewalling and routing should be handled by OPNSense.

My understanding was this also passed my WAN IP to OPNSense. That does not appear to be the case as OPNSense still needed to use an internal IP address on the WAN side and I see a lot of traffic on the ONT firewall logs. I also had to set some additional port forwarding rules on the Calix when experimenting with NextCloud. 

