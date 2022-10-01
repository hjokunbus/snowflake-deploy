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
over multiple hops from entry nodes to exit nodes, every connection secured by
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
device is active.

# Consider supporting TOR

It helps a great deal to become part of the TOR network with your devices. It
also helps to support the project itself with a donation. Because privacy
should be a human right.

[https://donate.torproject.org/](https://donate.torproject.org/)

# Licence

This software is in the public domain.