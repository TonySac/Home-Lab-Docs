---
title: Network
parent: Hardware
nav_order: 1
posted: 2024-09-20
updated: 2024-12-12
# Ok needs links to config sections when completed. Pics of network case. and diagram
---

{: .note}
UNDER CONSTRUCTION

# Networking Hardware

My home came pre-equipped with some decent enterprise grade networking equipment. I further leveled that up with an OPNSense router. I'm also lucky enough to have a cheap, fast, and reliable fiber connection. Im paying $39/month for 100 Mbps. However, as of this writing Ookla Speedtest is reporting almost 500 Mbps down and 300 Mbps up from my WiFi connected laptop.

![Ookla speed test results](/assets/speed_test.png)

## Modem

Nothing special here. I'm using the ISP provided Calix 844E-1 ONT/router combo. Originally, I used this as my DHCP server until I added the OPNSense router. That required some config magic on the Calix you can read about [here](/docs/network_configs/modem.html).

## Router

I picked up a cheap Firebat T8 dual NIC box off AliExpress to run OPNSense. It has the following specs:

 - Intel Celeron N5095 2.00 GHz Quad Core CPU
 - 8 GB RAM
 - 256 GB SSD HD
 - 2x Real-Tek Gigabit NICs (I know...)

More information on my OPNSense configuration can be found [here](/docs/network_configs/OPNSense.html).

## Switches & APs

### Ruckus ICX 7150-C12P PoE Switch

This is a pretty solid switch with a lot of enterprise functionality. I'm able to tag VLAN ports and power quite a few devices. I've got a walkthrough of some of the configuration in the network config section of these docs.

### Ruckus R510 Wireless AP

This bad boy gives WiFi coverage through my house. I've set it up to broadcast various SSIDs for private, guests, and IoT. More information on the configuration is in the network config section.


### Nicgiga 8 Port PoE Switch

Talk about a dumb switch. This thing is just a simple PoE switch I set up as a satellite switch on a VLAN for some cameras.
