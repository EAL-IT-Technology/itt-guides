---
layout: guide
date:   2017-05-30 21:00:39 +0200
title:  How do I set up a jump host?
categories: tech
status: beta
values:
  router_ext_ip: 10.0.0.100
  router_ssh_port: 22
  jumphost_ip: 192.168.1.20
  jumphost_ssh_port: 22
  jumphost_user: jumper
  internal_ip: 192.168.1.100
  internal_user: myuser
---

# Use case fro Jump host

A jump host is usually a host that has an sshd running and allows users to connect, and also allows ssh connections from the device.

(insert nice diagram here)

In the IPv4 scenario, the router has made a port forward from its outside interface on port 22 to port 22 on the interface of the jumphost.

In the IPv6 scenario, the router will be configured to block all connections, except the one going to the sshd on the jump host.

This way only one devices services are exposed to the internet.

This is very convinient, and work very well with key based ssh login.


# Variables used:

Variables used in the example:
* router_ext_ip: {{page.values.router_ext_ip}}
* router_ssh_port: {{page.values.router_ssh_port}}
* jumphost_ip: {{page.values.jumphost_ip}}
* jumphost_ssh_port: {{page.values.jumphost_ssh_port}}
* jumphost_user: {{page.values.jumphost_user}}
* internal_ip: {{page.values.internal_ip}}
* internal_user: {{page.values.internal_user}}


# Setup a jump host

The process

1. Create a default Debian/jessie installation with the hostname "jumphost"

    This has the ssh service installed by default

    (we need a guide for this)

2. As root on jumphost, run `adduser {{page.values.jumphost_user}}` and set a password

    This creates the user we will use for jumping.

3. Create a port forward on the router from the routers outside interface on port {{page.values.router_ssh_port}} to the jump host interface on port {{page.values.jumphost_ssh_port}}.

    (we need a guide for this)

# Test #1

1. As a common user on an external machine, run `ssh -p {{page.values.router_ssh_port}} {{page.values.jumphost_user}}@{{page.values.router_ext_ip}}`

    This will log onot the jump host

2. run `ssh {{page.values.internal_user}}@{{page.values.internal_ip}}`

    This will connect you from the jumphost to the internal device


# Test #2

1. As a common user on an external machine, run `ssh -o ProxyCommand="ssh -W %h:%p  -p {{page.values.router_ssh_port}} {{page.values.jumphost_user}}@{{page.values.router_ext_ip}}" {{page.values.internal_user}}@{{page.values.internal_ip}}`

    This will connect you to the internal through the jumphost - all in one line


# Test #3 - using openssh version >= 7.2

1. As a common user on an external machine, run `ssh -J {{page.values.jumphost_user}}@{{page.values.router_ext_ip}}:{{page.values.router_ssh_port}} {{page.values.internal_user}}@{{page.values.internal_ip}}`

    This will connect you to the internal through the jumphost - all in one line


# Remarks
In this example we have very limited security. Please check further reading links for more info.

# Further reading

(some links here would be nice as weel as suggested other guides)

* Passwordless login using keys
* ssh config files
* [Jump host cookbooks](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts)
