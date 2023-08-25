---
title: Port Forwarding in UTM
slug: UTM-port-forwarding
date: 2023-08-25
description: A quick guide to setting up port forwarding UTM
---

This is intended to be a brief guide to setting up port forwarding for a virtual machine in UTM. It took me longer than I would like to admit to figure out how to do it, as it was less obvious than in Virtual Box. I use port frowarding to be able to connect to headless virtual machines of ssh. (Bonus tip: the only way to run a headless VM in UTM is to remove the display from it in the edit menu)

Assuming you already have a virtual machine set up, right click it in the menu on the left side of thescreen and select "Edit".

![Network Settings](/images/UTM_Port_Forwarding/Network.png)

Select "Network" under the "Devices" section, and make sure the network mode is set to "Emulated VLAN".

![Network Settings](/images/UTM_Port_Forwarding/Network-Mode.png)

You should now see the "Port Forwarding" option underneath "Network". When you click on "Port Forwarding" select New at the bottom right, and configure it however you want. In my case that involved forwarding port 22 to another port on the host machine (I generally use 8022).

![Network Settings](/images/UTM_Port_Forwarding/Port-Forwarding.png)

__Remember:__ choose a port >1024 to avoid conflicting with the privaliged ports on your computer.

I hope this helps someone!

-Korben
