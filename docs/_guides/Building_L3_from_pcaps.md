---
date: 2017-09-29 12:00:00 +0000
layout: guide
title:  Building layer 3 diagrams from PCAP files
categories: tech
status: beta
---

Building layer 3 diagrams from PCAP files
================================================

Wireshark, tcpdump and many other network tools are able to save the raw packages to file. The default file format for that is PCAP files. As with most network traffic, this is a gold mine of information about the network.

There exists a lot of automated tools to extract e.g. html, images, passwords, topologies and sop on from PCAPS. This text is about how to do it manually using wireshark.

The official wireshark website is [here](https://www.wireshark.org/). If you are on a linux machine, wireshark is in the repositories and can be installed using `apt-get install wireshark` or similar.

Knowing what you want out of the pcackage dump will help prioritize the effort. Especially for large dumps, there will be so much information, that going through everything is not doable. Also, some protocols are obscure, and will require a lot of effort to look into.

We will assume that we are interested in creating a L3 diagram of IPv4.

1. Download the PCAP file

2. Open it in Wireshark

3. Get an overview of devices

    To create the L3 diagram, you need the list of IP addresses.

    Open `Statistics -> Endpoints`. This shows all Ethernet, IPv4, IPv6, TCP and UDP endpoints in the capture.   

    Divide devices by IP address into (at least) 3 groups: `internet` (ie. non-[RFC 1918](https://tools.ietf.org/html/rfc1918) addresses aka. public addresses), `local LAN` (if applicable) and `other private`.

    `Mulitcast` and `broadcast` addresses are not devices, but virtual addresses - looking into that traffic will say a lot about the sender, not the receiver.

4. Determine device type

    Still on `Statistics -> Endpoints`, the tabs TCP and UDP will tell which services are accessed on a given IP address.

    This is the baseline for a qualified gues as to what the pupose of a give device is. Examples:
    * UDP/53: DNS
    * TCP/80: HTTP, web
    * TCP/443: HTTPS, web
    * UDP/123: NTP
    * UDP 67,68: BOOTP, DHCP
    * TCP/22: SSH
    A list of "wellknown ports" are found [here](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)

    Note that TCP and UDP connections always have two port number: one for the client and one for the server. Clients *usually* have very high numbers like 20.000+, while servers serve at lower port number mostly below 1000.

4. Protocols

    Wireshark offer a breakdown of the protocols, using `statistics -> protocol hierarchy`.

    This will tell if any interesting protocols are in use.
    * ARP requests tell you which deveices are on `local LAN`
    * STP, RIP, LLDP will tell you about infrasturucture devices
    * DNS, LLNMR, MDNS, NBNS and others are nameservices, which will tell the name of a given device
    * Telnet, HTTP and FTP are un-encrypted protocols and all traffic (like passwords) are directly readable

    Note that wireshrk supports "right-clicking", which gives access to `apply as filer -> selected`, which will limit the packages whown in wireshark.
