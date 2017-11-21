---
title: Running Jobs with SLURM
author: Jessica Chung
date: '2017-08-11'
slug: running-jobs-with-slurm
categories: []
tags: []
weight: 1
description: 'Documentation on how to run SLURM jobs.'
---


Using a computer cluster with other users means sharing resources. SLURM 
(Simple Linux Utility for Resource Management) is a commonly used job scheduler
that manages a queue where you submit your jobs and allocates
resources to run your job when resources are available.

The documentation on using SLURM at Melbourne Bioinformatics is quite 
comprehensive and can be found
[here](https://www.melbournebioinformatics.org.au/documentation/running_jobs/slurm_x86/).


## Checking the status of your jobs

### squeue

You can view information about jobs in the SLURM queue with the `squeue`
command. View the help message with `squeue --usage` or the manual with 
`man squeue`.

```bash
# List all jobs in the queue
squeue

# List all jobs for account UOM0041
squeue --account=UOM0041

# List all jobs in the queue for user jchung in long format
squeue -l -u jchung
```

If you're using snowy or barcoo, you can also use the `showq` command.

#### scontrol show job

If you want information regarding a specific job id, you can use `scontrol`.

```bash
scontrol show job <job-id>
```

#### sacct

You can check the status of recently finished jobs with `sacct`.

```bash
sacct
```

#### sinfo

You can also view the status of the nodes in the cluster with `sinfo`.

```bash
# Show status of all nodes
sinfo -Nel
```

If you want more information about a specific node, you can use `scontrol`.

```bash
# View information on the master node
scontrol show node master
```


## Running your jobs

### sbatch

Most of your jobs will be sumbitted to SLURM via `sbatch`. The commands that
you want to run need to be written in a script (a plain-text file that we'll
discuss further below), saved to a location, then submitted using `sbatch`.

```bash
# Print the help message from sbatch
sbatch --help

# Submit your script by specifying the name of your script
sbatch my-script.sh
```

### sinteractive

You can use the `sinteractive` command to run your job in an interactive
session. When SLURM allocates your job resources, you will be provided with
an interactive terminal session. It is recommended to use sinteractive in
conjunction with a terminal multiplexer such as GUN Screen so the job won't
terminate if you disconnect from the server.

```bash
# Print the help message for sinteractive
sinteractive --help

# Submit a job with the default parameters
sinteractive

# Submit a job with 4 CPUs, 16 GB memory, and wall time of 1 day
sinteractive --ntasks=1 --cpu-per-task=4 --mem=16384 --time=1-0:0:0
```

Note that the memory amount is specified in MB.

### scancel

You can cancel a running job or a job in the queue with `scancel`.

```bash
scancel <job-id>
```

## Writing a SLURM script

For beginners, I recommend using the 
[job script generator](https://www.melbournebioinformatics.org.au/jobscript-generator/)
written by Melbourne Bioinformatics.
If you're using one of the PEARG clusters on the Nectar cloud (i.e. mozzie or 
rescue), you can ignore the "Project ID" and the "Modules" field.

Here's an example of a simple SLURM script running on the mozzie server.

```bash
#!/bin/bash
#SBATCH --job-name=denovo_map
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8

denovo_map.pl \
    -m 3 -M 2 -n 1 -T 8 -b 1 -S \
    -o denovo_map_m3_M2_n1_2017-11-09 \
    -s ../processed_radtags/sample-1.fastq.gz \
    -s ../processed_radtags/sample-2.fastq.gz \
    -X "populations: --vcf"
```

The first line of the script must specify the interpreter the script will be
executed with such as `bash` or `sh`. Keep this as `#!/bin/bash` unless you
have reason to change it.

Each line starting with `#SBATCH` is an option that SLURM's `sbatch` command 
uses. You can get view all available options with `sbatch -h` or by viewing 
the man page with `man sbatch`.

The most common `#SBATCH` options you'll most likely be using are:

* `--job-name=XXX`: You should always specify a job name for your job
* `--nodes=1`: In most cases, you should be requesting one node so all the
  requested CPUs are on the same node.
* `--ntasks=1`: In most cases you'll be running one task per job
* `--cpus-per-task=X`: Specify the number of CPUs to request.

You can also direct your stdout and stderr into defined files:

* `-output my-file-%j.out`
* `-error my-file-%j.err`

If you're using barcoo or snowy, you'll also need to specify memory in MB with:

* `--mem=XXXXX` for jobs using multiple CPUs, or
* `--mem-per-cpu=XXXX` for single CPU jobs.

With barcoo and snowy, you'll also need to specify the partition, and a time limit:

* `-p main`: The partition is called 'main'
* `--time=D-HH:MM:SS`: Time limit given for the job. If the job exceeds the time,
   it is automatically terminated.

Here's an example of a SLURM script for barcoo.

```bash
#!/bin/bash

# Partition for the job:
#SBATCH -p main

# Account to run the job:
#SBATCH --account=VR0002

# Multithreaded (SMP) job: must run on one node
#SBATCH --nodes=1

# The name of the job:
#SBATCH --job-name="test-job"

# Maximum number of tasks/CPU cores used by the job:
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8

# The amount of memory in megabytes per process in the job:
#SBATCH --mem=32768

# The maximum running time of the job in days-hours:mins:sec
#SBATCH --time=0-1:0:00

# Run the job from your home directory:
cd $HOME

# The job command(s):
sleep 10
```

When using barcoo and snowy, don't forget to `module load` the software you
need into your environment path.
