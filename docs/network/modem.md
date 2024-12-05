# Modem

Lets start with my ISP & modem setup. I have a fiber connection that terminates in my house at a Calix 844GE-1 ONT & router combo.

Its a basic enough device but worked fine in the begining when I used it as a DHCP server. Now that I've upgraded to OPNSense, I needed a way to pass my WAN thrugh to the OPNSense box.

Unfortuanlly, I cannot find an easy way to place this ONT in bridge mode. I've heard of some users having success calling their ISP and having it done that way. I elected to use the DMZ method. 

Here is how I've setup my ONT. First assumming you have interent, access to the admin GUI and the OPNSense box is plugged into the ONT

Under the quick start menu, I set static DNS servers to some of the public availbe ones. I'm using googles 8.8.8.8 and cloudflare 1.1.1.1. This ensures the ONT should always have DNS resoultion & internet access.

I configured a wireless network SSID and password. Then in the wireless settings, I turned on the 2.4G radio only but disabled broadcasting.  I did this so I always have a wireless backdoor into the ONT admin interface should somethiing go sideways.

Moving onto advanced settings, I changeed the DHCP addressing range. The default is `192.168.1.0/24` I chose something outside the default ranges to make sure there was no conflicts down the road say `192.168.12.0/24` for example. This gave the ONT an IP of `192.168.12.1`. I then created a DHCP reservation for the OPNSense box and one for my laptop. The only device that should ever be connected to the ONT is the hardwired OPNSense router, and maybe my laptop. Since they both have DHCP reservations, I can quickly tell if somethign else was connected.

Tip/NOTE
I beleibe I can also narrow the IP addressing range from the ONT admin interface. This can further restrict the devices able to connect to the ONT's network.

Under Securty I changed the default admin credentials. Then I enabled and  placed the OPNSense rotuers DHCP reservation in the DMZ.

I also checked a few other securty features such as maxing the ONTs firewall settings, disabling UPnP, and disabling remote managemnet.