---
title: Installing Software
author: Jessica Chung
date: '2017-09-29'
slug: installing-software
categories: []
tags: []
weight: 2
description: 'How to install software on our servers.'
---

If you want a particular piece of software installed on `mozzie` or `rescue` 
you can email me at [jchung@unimelb.edu.au](mailto:jchung@unimelb.edu.au).
Anyone is also free to compile and install software in their personal directories.

Installing software on Linux can be challenging. Sometimes it's as easy as a
downloading a pre-compiled binary file and sometimes you're stuck in
[Dependency Hell](https://en.wikipedia.org/wiki/Dependency_hell). There
are also be many different ways to install software depending on which form
it comes in. The most common ways you should use listed below.

-----

## Downloading binaries or jar archives

If the software is pre-compiled or is a java archive (ending in *.jar), you
can just download it to your directory and run it.

For example, let's say you want to install the latest version of Bowtie2
because the bowtie already installed on the cluster doesn't have the new
feature you want.

You would usually search for the software in your favourite search engine,
then make your way to the download page. Bowtie2 is hosted on Sourceforge
and has pre-compiled binaries, so we'll download the software from there.

The [Bowtie2 2.3.3 directory](https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.3/)
on Sourceforge currently has three items:

- bowtie2-2.3.3-macos-x86_64.zip
- bowtie2-2.3.3-linux-x86_64.zip
- bowtie2-2.3.3-source.zip

The first two items contain binaries for MacOS and Linux respectively.
The "x86_64"refers to the architecture it's meant to run on. The last file
is an archive containing the source code if we want to compile it ourselves.

Since our cluster runs Linux, we can download `bowtie2-2.3.3-linux-x86_64.zip`.
Right click on the link and copy the link address so we can download it to
the server.

```bash
# Login and change to a directory where you want to store your software
cd software
# Download the file
wget https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.3.3/bowtie2-2.3.3-linux-x86_64.zip/download -O bowtie2-2.3.3-linux-x86_64.zip
# Unzip the directory
unzip bowtie2-2.3.3-linux-x86_64.zip
# Enter the directory and see what's inside
cd bowtie2-2.3.3 && ls
# Run and view the help options of bowtie
./bowtie2 --help
```

Java archives are also simple to run. Just download the .jar file, and
execute something like:
```bash
java -jar <my_program>.jar
```

Sometimes you'll need to specifiy the memory required like so:
```bash
# Specify 4gb as the maximum heap size
java -Xmx4g -jar <my_program>.jar
```

-----

## Conda packages

[Conda](https://conda.io/docs/) is a package manager written in Python and is
available for use on our clusters. Package managers make installing
easy by automating the process and handing dependencies. Many bioinformatics 
tools have been wrapped for Conda installation and are in the 
[bioconda](https://bioconda.github.io/) channel.

You'll need to create your own virtual environment to use Conda, since you
won't have write permission to install software in the default location.
A virtual environment is an environment where you have your own isolated copy 
of Conda and your own software packages that you installed via Conda. Virtual
environments work by appending the virtual environment's bin directory to
your `$PATH`.

You can learn more about Conda [here](https://conda.io/docs/user-guide/getting-started.html).

If you're using the Melbourne Bioinformatics clusters, you'll need to 
`module load` Python into your environment path first.

```bash
# If you're using barcoo
module load python-intel/3.6
```

Let's create a new Conda virtual environment and install a package.

```bash
# Create a virtual environment called my_new_env
conda create -n my_new_env

# Activate the enviroment
source activate my_new_env

# Your command line prompt should now start with (my_new_env) $

# Look at your path and see the first bin directory is your
# conda environment in your home directory
echo $PATH
```

You can manage packages using the `conda` command.

```bash
# Print conda help
conda -h

# List conda packages
conda list
```

You can install packages with `conda install`. For example, 
[bioawk](https://github.com/lh3/bioawk) is available in the 
[bioconda channel](https://anaconda.org/bioconda/bioawk) and you can install it
like so:

```bash
# Install bioawk from the bioconda channel
conda install -c bioconda bioawk
```

When you're finished using your software in conda, you can exit the virtual
environment with:
```bash
source deactivate
```

And when you need your virtual environment again, you can reactivate it with:
```bash
source activate <my-environment-name>
```

-----

## Compiling from source

Compiling from source is another way to install software. Sometimes, only the
source code is provided and in this case, you'll need to compile the software
yourself.

A common case is that the source code of the program you want to install is 
available on GitHub. Often, there are installation instructions in the README 
or INSTALL file which you can follow.

In the most simple case, a `make` command will run a Makefile and compile the 
software into a binary file which you can execute. Let's compile 
[bwa](https://github.com/lh3/bwa) as an example.

```bash
# Clone the repository
git clone https://github.com/lh3/bwa.git
# Change directory
cd bwa
# Compile
make
```

A new file called `bwa` should be in the directory which you can run with
`./bwa`.

Software may also specify it needs to be built with `./configure`, `make`, then
`make install`. The configure script checks the environment the software is
to be built in and checks dependencies. Typically, you can also specify 
additional options when running `./configure` such as `--prefix=/home/my_username/bin`
to specify where to install the software. Running the configure script should
output a Makefile. Running `make` will built the software and `make install`
will copy the executable files into the default or specified directory. 

You can read more about using configure, make, and make install
[here](http://www.codecoffee.com/tipsforlinux/articles/27.html) and
[here](https://robots.thoughtbot.com/the-magic-behind-configure-make-make-install).


