---
title: Using sFTP with Mediaflux
author: Jessica Chung
date: '2020-02-21'
slug: using-mediaflux/mediaflux-sftp
categories: []
tags: []
hidden: true
description: 'Using sFTP to upload and download files from Mediaflux'
---


-----

### Command-line sFTP

If you want to transfer files between the PEARG servers (e.g. mozzie) and
Mediaflux, the easiest way to do this is to use sFTP on the command line.

If you're transferring large files, I recommend you use sFTP in a screen
session so you can detach it and leave it running in the background.

#### Downloading files from mediaflux

Let's say I'm interested in a particular tarball which is located at   `/Volumes/proj-hoffmann_data-1128.4.49/data/QA_library3_DPS_INC_KL.tar`  
in Mediaflux and want to download it to my current working directory.

```text
# First navigate to where you want the downloaded file to be stored.
cd /path/to/my/project/data

# Then sFTP into the mediaflux server (change the credentials to your username)

# If you have a staff unimelb account:
sftp -P 21 -o User=unimelb:username mediaflux.researchsoftware.unimelb.edu.au
# Authenticate using your university password

# Alternatively, if you have a student unimelb account:
# sftp -P 21 -o User=student:username mediaflux.researchsoftware.unimelb.edu.au

# Navigate to directory that has the file of interest
cd /Volumes/proj-hoffmann_data-1128.4.49/data

# List all files in the current directory
ls

# Download the file to your current working directory
get QA_library3_DPS_INC_KL.tar

# Disconnect from the mediaflux server
exit
```

#### Uploading files to Mediaflux

Let's say I have a file on the mozzie server, `MPP_allsubreads.fastq.gz` that I
would like to upload into Mediaflux to the location  
`/Volumes/proj-marsupial_genomics-1128.4.19/Burramys/Assembly`

```text
# First navigate to where you want the downloaded file to be stored.
cd /path/to/my/project/data

# Then sFTP into the mediaflux server (change the credentials to your username)

# If you have a staff unimelb account:
sftp -P 21 -o User=unimelb:username mediaflux.researchsoftware.unimelb.edu.au
# Authenticate using your university password

# Alternatively, if you have a student unimelb account:
# sftp -P 21 -o User=student:username mediaflux.researchsoftware.unimelb.edu.au

# Navigate to directory where you want to upload the file to
cd /Volumes/proj-marsupial_genomics-1128.4.19/Burramys/Assembly

# List all files in the current directory
ls

# Upload the file from your current working directory
put MPP_allsubreads.fastq.gz

# Disconnect from the mediaflux server
exit
```

-----

### sFTP clients

If you want to transfer files between your local computer and Mediaflux, you 
can also use graphical sFTP clients such as WinSCP, FileZilla, and Cyberduck.

You'll need to connect to the `mediaflux.researchsoftware.unimelb.edu.au` server
using port 21 (note: if port 21 doesn't work, try port 9003).

If you have a unimelb staff account, your username should be `unimelb:username`,
and if you have a student account, `student:username`.

Example connecting using Cyberduck:

<img src="/metadata-documentation/static/sftp_cyberduck.png" alt="" width="70%" height="70%"/>

Example connecting using WinSCP:

![](/metadata-documentation/static/sftp_winscp.png)

