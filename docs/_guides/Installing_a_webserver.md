---
layout: guide
date:   2017-05-30 21:00:39 +0200
title:  How do I install a webserver
categories: tech
status: beta
---

# Use case

Webservers are widely used to serve html pages with or without dynamic content. Start [here](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server) for a quick introduction.

It is also a very good example service for minimal servers in a network system to illustrate connectivity and test [port forwards](https://en.wikipedia.org/wiki/Port_forwarding).

This guide is for Debian (and ubuntu based systems) and we will install [lighttpd](https://www.lighttpd.net/), which is a lightweight webserver.


# Installing

1. Log in as root

    On Ubuntu, use `sudo bash` to get a command prompt as root.
    On Debian, use `su`and supply root password

1. Run `apt-get update`

    Do this to update the repository list. It just solves a lot of issues before they arize.

2. Run `apt-get install lighttpd`

3. Run `nano /var/www/html/index.html`and paste the following

    ```
    <!DOCTYPE html PUBLIC "-//IETF//DTD HTML 2.0//EN">
    <HTML>
       <HEAD>
          <TITLE>
             A Small Hello
          </TITLE>
       </HEAD>
    <BODY>
       <H1>Hi</H1>
       <P>This is very minimal "hello world" HTML document.</P>
    </BODY>
    </HTML>
    ```

    This createsCreate your own start page,

3. Feel awesome



# Test

1. On the server, run `w3m http://localhost`

    This gives you text mode version of the html page you installed

2. On another machine, run `wget http://<ip address>/index.html`, where <ip address> is the address of the server

    This will download `index.html`. To see it, use `cat index.html`

3. Start your browser and got to `http://<ip address>`


# Remarks

HTTP is bad for privacy, use the encrypted verison instead. [Let's encrypt](https://letsencrypt.org/) may help you with that.

# Further reading

(to come if they are added...)
