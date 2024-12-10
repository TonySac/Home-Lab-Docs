---
title: HAOS19
parent: Home Assistant
nav_order: 1
# posted: 2024-09-21
---

{: .note}
UNDER CONSTRUCTION

# Home Assistant

I have been using Home Assistant in some capacity since 2019. Initally it was a way to consolidate all of my smart home devices into one app. Now it serves as my entire home automation hub. I've developed automations for streaming music, notifications for motion detection, and of couse moblie dashboards for controlling lights.

Because of all the nuances with HomeAssistant, I feel its own section is justifed here.

Recently I moved from local and VPN only access to HomeAssistant Cloud and Nabu Casa. It's such a streamlined way to safely ensure remote access to the system. I probably could have set up a reverse proxy on my own but I'm not confident enough in that skill set to garanutee the security. Plus the Nabu Casa subscruption wont break the bank and is a good way for me to support a project I've grown to love.

# Initallization

Once the Home Assistant VM boots, the console should display the CLI along iwth the machine's IP address. Use the IP address and port 8123 to access the UI.

The first initalization will ask some simple questions about device location and error reporting. You will also be prompted to create a login. I personally like to create an adminstrator account. I use this for all of my admin tasks and modifcations. I then create seperate user accounts for myself, wife, and anyone or thing that needs to access Home Assistant. I feel this gives me a little better control.

Pop over to user settings and enable advanced mode, double check TZ settings.

dashboard, penicl, hamburger and take control with empty dashboard