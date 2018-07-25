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


Download the 3 files within and save them into a directory (all in the same one)
--

Vmware
======
__

Open your vmware software, either on your user or as root depending on permissions for virtual machines.

Opening vmware as root from the command-line can be done with the command <sudo vmware> or <su root && vmware>

When vmware is open, **MAKE SURE NOT TO HAVE HIGHLIGHTED "Shared VMs" INSTEAD HIGHLIGHT "My Computer"**

1. Click on "File > create new virtual machine" Or just ctrl + n

2. Choose "Typical (recommended)" (depending on your vmware version), click next .

3. Choose "I will install operation system later"

4. Choose the option 6. Other, and find the " Version: FreeBSD 11 64-bit "
This part is no "too" important what you choose, it is somewhat nessacary to how vmware suggest to format the disks.
For example if windows is chosen install a linux distro, fat32 will be suggested, and possible not the linux structure you want.

5. Enter a name and save it somewhere.

6. Choose disk size to be 1.0 GB and **STORE VIRTUAL DISK AS A SINGLE FILE"

7. Finish the installation.

__

Now to install the Vsrx image
-

1. Click on " Edit virtual machine settings"

2. Highlight Hard Disk and click on remove.

3. Click on add, and choose Hard Disk

4. ** Not sure which type to choose here ** Choosing IDE

5.  Click on "Use existing Virtual disk" 

6. Click on browse, and find the directory with your vSRX files.

7. Find the file that has a ending om " .vmdk" and choose Open

8. Click Finish and choose "keep Existing Format"
