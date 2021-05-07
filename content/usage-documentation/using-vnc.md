---
title: Using VNC
author: Jessica Chung
date: '2021-05-07'
slug: using-vnc
categories: []
tags: []
weight: 2
description: 'How to connect to the server using VNC'
---

You can also connect to the `mozzie` or `rescue` server using VNC, a graphical 
desktop-sharing system, from your internet browser.

-----

## Setup

You'll only need to follow these setup instructions once.

First, SSH into the server and create a password using `vncpasswd`. Note that
any password over 8 character is automatically truncated to a length of 8.

```bash
vncpasswd
```

Follow the prompts to setup and confirm your password. You don't need to setup 
a view-only password.

```
# Using password file /mnt/galaxy/home/jess/.vnc/passwd
# VNC directory /mnt/galaxy/home/jess/.vnc does not exist, creating.
# Password:
# Warning: password truncated to the length of 8.
# Verify:
# Would you like to enter a view-only password (y/n)? n
```

If you ever want to change your password, you can use the `vncpasswd` utility 
again.


Then copy the `xstartup` script to your home `.vnc` directory.

```bash
cp /mnt/galaxy/shared/scripts/xstartup ~/.vnc/
```

-----

## Running vncserver

Each time you want to use VNC, you'll need to start and stop your personal VNC
server.

To start the server, use the `vncserver` command.

```bash
vncserver
```

You'll get something like the following output printed out to the console:

<img src="/pearg_documentation/usage-documentation/static/vncserver_session.png" alt="" width="90%" height="90%"/>

Keep note of the session number that is on the first line. In the example above,
the session number is 3.

In your internet browser, head to your server's homepage 
([mozzie](http://115.146.86.169/), 
[rescue](http://115.146.86.14)), and
click on the corresponding link under the VNC heading.

<img src="/pearg_documentation/usage-documentation/static/vnc_session_links.png" alt="" width="70%" height="70%"/>

(If your session number is greater than the number of sessions available 
on the homepage, please contact Jess at
[jchung@unimelb.edu.au](mailto:jchung@unimelb.edu.au).)

<img src="/pearg_documentation/usage-documentation/static/novnc.png" alt="" width="70%" height="70%"/>

Click the connect button and type in your VNC password.

You should now be connected to the server via VNC.

<img src="/pearg_documentation/usage-documentation/static/novnc_xfce.png" alt="" width="70%" height="70%"/>

When you're done using VNC, stop the VNC server by with `vncserver -kill` and by specifying the session number like so:

```bash
vncserver -kill :3
```

Please shut down your vncserver when you're finished with it since there are
a limited number of sessions that can be used simultaneously.

Note that you can only have one instance of vncsesrver that works. Multiple 
instances will result in a blank grey screen.

If you ever forget the session number of your vncserver session, or want to
check how many sessions you have running, you can check your `~/.vnc` directory
for files ending with `*.pid`. Each running session will create a `.pid` file
that has the session number in the filename (e.g. `mozzie:3.pid`).

If you need any help getting VNC to work, or have any questions, don't hesitate
to contact Jess.
