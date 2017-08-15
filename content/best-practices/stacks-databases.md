---
title: Stacks Databases
author: Jessica Chung
date: '2017-08-11'
slug: stacks-databases
categories: []
tags: []
weight: 5
description: 'Best practises for working with Stacks databases.'
---

```text
#
# Note: This document is a work in progress and the commands are untested
#
```

## Database management

Databases are usually large in size and we have limited space on our clusters.
To remedy this, please remove any databases you don't need. If you have a
database older than 3 months in the system, you will be asked to clean up
your old databases.

### Naming your databases

Make sure to include your name and the date your database was created in your
database name. Some examples of good database names are:

```text
alice_mozzie_x123_2017-03-04
bob_possum_filtered_2017-07-01
carol_AaegL2_males_2017-01-22
```

{{% notice warning %}}
If your name and a creation date is not included in your database name, your
database may be deleted without warning.
{{% /notice %}}


### Removing databases

Delete databases by using the SQL `DROP DATABASE` statement.

```bash
mysql -e "DROP DATABASE jess_radtags_2017-08-15"
```

### Backing up databases

You can also backup your database with the `mysqldump` command. The output is
in plain-text, so use `gzip` to compress the file to save space.

```bash
mysqldump --databases jess_radtags_2017-08-15 \
    | gzip > ~/my_backups/jess_radtags_2017-08-15.sql.gz
```

### Restoring a database from backup

You can restore your saved databases by importing your file into MySQL.

```bash
mysql jess_radtags_2017-05-02 < ~/my_backups/jess_radtags_2017-05-02.sql
```

-----

### Running Stacks on clusters which don't allow databases

If you're using the barcoo cluster for your analysis, you won't be able to 
load your catalog to a database on the cluster. This means you'll need to 
do your computation (on barcoo) separately to a machine that alows database
access.

#### On barcoo

If you're using `ref_map.pl` or `denovo_map.pl` you can use the `-S` option
to disable all database interaction. The output from this step should be
many tsv files.

Example output:

```text
batch_1.catalog.alleles.tsv
batch_1.catalog.snps.tsv
batch_1.catalog.tags.tsv
batch_1.haplotypes.tsv
batch_1.hapstats.tsv
batch_1.markers.tsv
batch_1.populations.log
batch_1.sumstats_summary.tsv
batch_1.sumstats.tsv
batch_1.vcf
mozzie-1.alleles.tsv
mozzie-1.matches.tsv
mozzie-1.models.tsv
mozzie-1.snps.tsv
mozzie-1.tags.tsv
mozzie-2.alleles.tsv
mozzie-2.matches.tsv
mozzie-2.models.tsv
mozzie-2.snps.tsv
mozzie-2.tags.tsv
...
```

#### Transfer your data

You'll need to transfer your output files from `ref_map.pl` or `denovo_map.pl`
to another computer which you have permission to create databases on. Since
tsv files are plain-text, it's good practice to compress them before transferring.

You can use a graphical FTP client or the command line to transfer files.
Here we'll use `rsync` with the `--compress` option to do transfer the files.

On barcoo, in an interactive slurm session, you can transfer the directory
called `catalog` with the following command:

```sh
rsync -av --compress --update --progress \
    catalog \
    <username>@<IP-address>:<path_to_my_project_directory>
```

replacing `<username>`, `<IP-address>`, and `<path_to_my_project_directory>`
with your relevant information.

#### Load the catalog with load_radtags.pl

On your machine which you have permission to create databases, load your
catalog with [`load_radtags.pl`](http://catchenlab.life.illinois.edu/stacks/comp/load_radtags.php).

```bash
# Create an empty database
mysql -e "CREATE DATABASE jess_radtags_2017-08-15"

# Load template tables
mysql jess_radtags_2017-08-15 < /usr/local/share/stacks/sql/stacks.sql

# Load RAD tags
load_radtags.pl \
    -D jess_radtags_2017-08-15 \
    -p catalog \
    -b 1
    -B -e "Description here" \
    -c
```


