# Simple playbook to deploy TOR snowflake

**Disclaimer:** This repository is not in any way or form connected to
Snowflake cloud nor the TOR project.

## What is TOR? What is Snowflake? And what is the connection between both?

As recent news have shown, free expression and free speech are very fragile
privileges far from being universal rights or law in each country. Our digital
communication can be used by autocratic governments to track dissidents, even
if our communication is encrypted. Meta data tells businesses and agencies who
we are and who we are talking to, when and from where.

TOR is an infrastructure to hide our communication profiles from authorities.
In short, volunteers run TOR nodes on their hardware which route your traffic
over multiple relays from entry nodes to exit nodes, every connection secured by
multiply layers of encryption (hence the name "the onion router") and routed
differently, i.e. even participants with malicious intentions are not able to
gather personal information in a way that makes it easy to deduce personal
profiles.

The list of entry points of TOR is made publicly available by the project. This
unfortunately again gives governments the opportunity to block TOR
communication, as we have seen in the recent past.

This is where Snowflake comes into play. TOR has some reserved entry nodes
up their sleeves. Those are communicated to TOR clients via protocols which
are commonly used for video streaming, while volunteers provide their hardware
to be proxies that bridge communication from the public internet to the TOR
entry nodes. With this method everyone now can provide a virtual entry node and
governments have no way to block TOR communication in particular.

If you want to learn more, please visit the
[project's website](https://snowflake.torproject.org/).

# Installation

## Prerequisites

This project was created for systems that use apt. It should be simple enough to
work on every platform that is derived from Debian. I have tested it on my
RaspberryPi with a RaspianOS-Bullseye installation. Other than that you should
look up the
[installation requirements for ansible control and managed nodes](https://docs.ansible.com/ansible-core/devel/installation_guide/intro_installation.html).

The targeted device needs Python installed and a running SSH service.
It helps to have SSH public key authentication in place. Otherwise you need to
give the playbook a hint that is should ask for passwords
[via CLI](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html).
The controlling device needs to have ansible installed.

I have already prepared a device in the inventory that should work out of the
box with a fresh installation of Raspian. If you use something different, edit
the [raspi.ini](inventory/raspi.ini) file as you wish.

## What's next?

Run `ansible-playbook snowflake.yml`.

That's it! It installs all the required packages, downloads and builds the
recent software, and creates and starts a service that will run as long as your
device is active. The result should look like this:

```
 $ sudo systemctl status snowflake
● snowflake.service - TOR snowflake proxy
     Loaded: loaded (/lib/systemd/system/snowflake.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2022-10-01 09:59:56 BST; 2h 55min ago
   Main PID: 5139 (proxy)
      Tasks: 7 (limit: 415)
        CPU: 1h 40min 15.254s
     CGroup: /system.slice/snowflake.service
             └─5139 /home/holger/snowflake/proxy/proxy > /home/holger/snowflake.log

Oct 01 12:45:35 testtarget nohup[5139]: 2022/10/01 11:45:35 connected to relay
Oct 01 12:45:59 testtarget nohup[5139]: 2022/10/01 11:45:59 OnClose channel
Oct 01 12:45:59 testtarget nohup[5139]: 2022/10/01 11:45:59 Traffic throughput (up|down): 11 KB|22 KB -- (52 OnMessages, 24 Sends, over 24 seconds)
Oct 01 12:45:59 testtarget nohup[5139]: 2022/10/01 11:45:59 datachannelHandler ends
Oct 01 12:45:59 testtarget nohup[5139]: 2022/10/01 11:45:59 sdp offer successfully received.
Oct 01 12:45:59 testtarget nohup[5139]: 2022/10/01 11:45:59 Generating answer...
Oct 01 12:46:01 testtarget nohup[5139]: 2022/10/01 11:46:01 OnDataChannel
Oct 01 12:46:01 testtarget nohup[5139]: 2022/10/01 11:46:01 Connection successful.
Oct 01 12:46:01 testtarget nohup[5139]: 2022/10/01 11:46:01 OnOpen channel
Oct 01 12:46:01 testtarget nohup[5139]: 2022/10/01 11:46:01 connected to relay
```

# Consider supporting TOR

It helps a great deal to become part of the TOR network with your devices. It
also helps to support the project itself with a donation. Because privacy
should be a human right.

[https://donate.torproject.org/](https://donate.torproject.org/)

## What else to consider?

First of all: Legally you're providing a service. But since Snowflake only
provides a way to connect to entry nodes you are not responsible for what
websites people visit through TOR. This may vary in your country and I'm not a
lawyer.

Second of all: The software is run with privileges of your user and also the
files will be placed into the home directory of the user you've chosen. Because
running services as root has to be avoided if humanly possible.

If your ISP provides only Dual Stack Lite (DSLite) Snowflake might not work as
good as it could (from my experience). If you have any issues with the
standalone proxy, please have a look into the
[currently open issues](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/snowflake/-/issues)
of the project.

# Licence

This software is in the public domain.
