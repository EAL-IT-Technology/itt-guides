---
date: 2018-08-25 23:00:00 +0000
layout: guide
title:  Install Vsrx on a linux machine using vmware
categories: vmware/Linux
status: beta
---

Installing the Vsrx on a linux machine using vmware
===================================================

This guide should only apply to linux distros, considering the process
for install is different depending on the OS.

This guide was done on VMware 14.x

--
Some prerequirements

1. Vmware installing 10.x or higher

2. As a very minimum 512 MB of ram to spare for the virtual machine

3. A CPU capable of running virtual machines.

--

First is to get the files needed to mount the vsrx.
In this example I will use the ones from the EAL fronter pages
This version of the Vsrx will be 12.1x

**NOTE this might be different depending on the semesters fronterpage

If there is not access to fronter, getting one from Junipers site is possible,
but with registration.

* Link for vSRX software

https://www.juniper.net/support/downloads/?p=vsrx#sw

--


Go to: oeait17eiC > 1st Semester > Data Communication > Software

If you can't navigate on fronter look below :-)


Inside the fronter page navigate to the section under "Entrance Hall" called: oeait17eiC

Click on the "1st Semester" tab.

Go into the files having the string: oeait17eiC > 1st Semester > Data Communication > Software


Download the 2 files with the format ( .vmdk and .ovf)
within and save them into a directory (all in the same one)
--

Avoid the .mf file
==================


Vmware
======
__

Open your vmware software, either on your user or as root depending on permissions for virtual machines.

Opening vmware as root from the command-line can be done with the command <sudo vmware> or <su root && vmware>

When vmware is open, **MAKE SURE NOT TO HAVE HIGHLIGHTED "Shared VMs" INSTEAD HIGHLIGHT "My Computer"**

1. Click on "File > Open" Or just ctrl + O

2. Navigate to the folder you saved the 2 files in, and select the junos-vsrx-12.1X47-D15.4-domestic.ovf

3. Choose a fitting name, and a location.

4. Click on import, and wait

5. You should now have a working vSRX (Try booting it for testing)

__


