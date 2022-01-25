---
title: Mediaflux Explorer
author: Jessica Chung
date: '2017-08-15'
slug: mediaflux-explorer
categories: []
tags: []
weight: 3
description: 'How to use Mediaflux Explorer.'
---

{{% notice warning %}}
This page has been deprecated. To use Mediaflux Explorer on the mozzie server, [start a VNC session]({{%relref "using-vnc.md"%}}), launch a terminal, and enter `mediaflux-explorer` to launch the application.
{{% /notice %}}


The Mediaflux service can be accessed via a Java applet (Mediaflux Explorer) or
via your web browser with [Mediaflux Desktop](https://mediaflux.researchsoftware.unimelb.edu.au/desktop/).
These clients allow you to view your data, transfer data, and edit metadata.

The Mediaflux Explorer Java applet should be used when transferring data and is
available on both [`mozzie`](http://45.113.232.220) and 
[`rescue`](http://45.113.233.108/) servers. Note that uploading large files
via the browser is unreliable and slow, therefore Mediaflux Desktop should not be
used for uploading.

Assuming you have your data stored on one of our servers
([`mozzie`](http://45.113.235.8) or [`rescue`](http://45.113.233.108/)) open 
your preferred internet browser and enter the IP address of the server into
the navigation bar.

You should be taken to the dashboard page that lists the services available.
Find the 'Lubuntu Desktop' service and click on the access link to use VNC.
This allows us to access the server using a graphical interface through a browser.

![](../static/dashboard_vnc.png)

Enter your credentials for your account to login. You may need to do this twice---
once to access VNC and again to login to the Lubuntu desktop.

<img src="../static/lubuntu_login.png" width=80%>

Logging in will bring you to the Lubuntu desktop where you should see icons
including a 'Mediaflux' icon. Double click it to launch Mediaflux Explorer.

![](../static/lubuntu_desktop.png)

Select the HTTPS protocol in the dropdown menu and enter 
`mediaflux.researchsoftware.unimelb.edu.au`
as the host. The port should automatically change to `443`.

In the 'Domain' field, enter `unimelb` if you have a unimelb staff account or
`student` if you have a unimelb student account. Then enter your unimelb
username (not your email) and password to sign in.

<img src="../static/mediaflux_login.png" width=80%>


