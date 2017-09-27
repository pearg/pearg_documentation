---
title: Backing Up Your Data
author: Jessica Chung
date: '2017-08-15'
slug: backing-up-your-data
categories: []
tags: []
weight: 10
description: 'Best practices for backing up your data.'
---

If you only have a single copy of your data, you're vulnerable to losing it.
A hardware failure or theft can lead to losing hundreds of hours of work or
irreplacable photos.

*"Don't worry--- I have a Time Machine backup,"* I hear you say. 
Having a Time Machine backup is a good first step, however, you're still at risk
in cases where you lose both copies in a house fire or if both your laptop
and Time Machine hard drive are stolen. 

Hard disk drives are also prone to failure.

<a href="https://www.backblaze.com/blog/hard-drive-reliability-update-september-2014"><img src="https://www.backblaze.com/blog/wp-content/uploads/2014/09/blog-fail-drives-manufactureX.jpg" alt="Hard Drive Failure Rates by Model" width=50% border="0" /></a>

One solution is to store a copy of your data remotely in the cloud. Storage 
services will also have redundancy measures in place to avoid data loss when 
hard drives inevitably fail.

A good rule to follow is the 3-2-1 rule for backing up your data.

{{% panel theme="success" header="The 3-2-1 rule for backups" %}}
The 3-2-1 rule for backup goes as follows:

- Have at least three copies of your data
- Use at least two different types of media for your copies
- At least one of your copies should be offsite
{{% /panel %}}


### Backing up your experimental data

Following the 3-2-1 rule, your sequencing data for your study should have at 
least three copies. A typical case would be:

- one copy on a external hard drive stored in the lab
- one copy on the volume attached to the server where you're doing your analysis
- one copy in Mediaflux labeled with appropriate
  [metadata]({{%ref "metadata-documentation/metadata-overview.md"%}})


### Cloud-based automated backup services

Having a remote backup for your computer is also a good idea. Services such as
[Backblaze](https://www.backblaze.com/hellointernet) can automatically backup
your computer, but they also have a monthly subscription fee at around $5 a month. 

An example of using the 3-2-1 rule for backing up your laptop would be:

- one copy on the SSD in your laptop
- one copy on a HDD with Time Machine backups
- one copy in the cloud using a cloud backup service such as 
  [Backblaze](https://www.backblaze.com/hellointernet)



