=======
Network
=======

| The real internet speed that I'm getting at the moment from my ISP [#]_ are 60 Mb/s download and 6 Mb/s upload in coaxial, since they dont want to offer me optic fiber.

Devices
=======

| At the moment I'm using the following devices.

- Modem
- TP-Link router
- TP-Link repeater
- Netgear router
- Multiple Cat 5 Ethernet cables


Configuration
=============

------------
Ip Addresses
------------

| LXCs and VMs are in the same physical server, but each one has its own IP and MAC addresses, so they are shown to the network as separate devices.
| The IP addresses of each LXC and VM are not going to be named or numbered so there won't be any security leak.

--------------
TP-Link Router
--------------

| It's the main router connected to the modem and all the networks devices. It can be configured through web GUI typing its IP in the browser.
| The main router serves as the DHCP server for the rest of the devices.
| 
| The ports needed to be open must be set in that router, which I'm not going to name for security reasons.
| To open a port simply go to *NAT Forwarding, Virtual Servers*. Then specify the internal and external port, the internal IP and the protocol.


No-Ip DDNS
----------

| Public addresses assigned by the ISP are **dynamic**, which means they change from time to time.
| 
| Static public addresses cost extra money and not all the ISPs offer them and are oriented for enterprises only.
|
| Instead of using a regular DNS server software like bind9 which is only useful for static addresses, I used **No-IP**.
| 
| No-IP is a dynamic DNS that will always point the public IP address of the router to a domain name, even if its IP changes.
| It offers up to 3 free dynamic domains.
| For this project I used the following domain names.

1. **A** record named **masterserver.serveminecraft.net**
2. **CNAME** record named **efrenthemaster.serveminecraft.net** with the target set as masterserver.serveminecraft.net
3. **CNAME** record named **masterstats.serveminecraft.net** with the target set as masterserver.serveminecraft.net

| To set it up I just went into the router GUI and then to *Network, Dynamic DNS*
| There I typed the A record domain name and No-IP login credentials. It takes a little of time to propagate the DNS. That can be checked `here <https://dnsmap.io>`__.

----------------
TP-Link Repeater
----------------

| The only reason why I'm using the repeater is because I haven't done a structured network cabling at home, so the only way to connect devices in a different floor is bringing internet through the power socket with a repeater. It doesnt require further configuration, just plug the transmitter to the TP-Link router and the power socket, and the receiver to the power socket in my room plugged to the Netgear router.

--------------
Netgear Router
--------------

| The repeater only comes with 2 RJ45 plugs and I have multiple devices in my room. The solution is configuring a router I had laying around to serve as a switch for now, since I dont have the 24 port gigabit switch yet.
| 
| It has 4 gigabit ethernet ports that are enough for the purposes of the project.
| To configure it as a switch I did the following steps.

- Plug the repeater RJ45 into one of its gigabit ethernet ports
- Disable DHCP server
- Change its IP to a non used one in the same subnet
- Disable WiFi channel

| After doing that simply plug the devices to the rest of the ethernet ports and it's done

.. rubric:: Footnotes

.. [#] Internet Service Provider



