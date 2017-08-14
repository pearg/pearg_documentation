---
title: Naming Files
author: Jessica Chung
date: '2017-08-11'
slug: naming-files
categories: []
tags: []
weight: 2
description: 'Best practices for naming files.'
---

This document describes best practices for naming files.

I highly recommend you read this Data Carpentary document on
[file naming](https://butterflyology.github.io/rr-organization1/01-file-naming/).

## Be descriptive

Good filenames should be precise. For example, a raw FASTQ filename received
from AGRF may look something like this:

```text
X54321-1_AB1XXXXXX_GAATTCGT-ATAGAGGC_L007_R2.fastq.gz
```

The filename contains a lot of information which is descriptive to the user and 
can be easily extracted programatically.

Just by looking at the filename and knowing what each field represents, we have 
the following information:

- Sample name: `X54321-1`
- Flowcell ID: `AB1XXXXXX`
- Index: `GAATTCGT-ATAGAGGC`
- Lane: `L007`
- Forward/Reverse: `R2`
- File format: `fastq`
- Compression: `gz`

Storing metadata in this fashion allows us to avoid mixing up samples and 
losing expensive sequencing data due to lost information.


## Be consistent

If you're storing metadata in filenames, it's good practice to be consistent
with what each field represents. Being consisent also means filenames are
sorted in a logical manner when listed alphabetically.

Good consistency:

```text
2017-02-07_cg_meeting_notes_with_alice.md
2017-02-14_cg_meeting_notes_with_bob.md
2017-02-21_cg_meeting_notes_with_alice.md
2017-02-28_cg_meeting_notes_with_carol.md
```

Bad consistency:

```text
14.02.17_bob_cg_meeting.md
21-02-alice-meeting-cg.md
carol_cg_meeting_notes_2017-02-28.md
cg_meeting_with_alice_2017-02-07.md
```

## Allowed characters

Avoid special characters. The only characters you should be using in your 
filenames are the alphanumeric characters (`A-Z`, `a-z`, `0-9`), underscores 
(`_`), periods (`.`), and dashes (`-`). Always start your filename with an
alphanumeric character.


## Avoid using spaces

Using spaces in filenames makes things difficult when working with UNIX.
Therefore, use underscores `_` and dashes `-` to separate words.

For example:

```text
sample-data-from-bob.txt
2017-03-03_raw_data_ID_A721BW.tar.gz
```

You can also use periods `.` for additional metadata information.

```text
sample-1.AaegL3.bam
sample-1.AaegL3.sorted.bam
sample-1.AaegL3.sorted.filtered.bam
```

## YYYY-MM-DD

The [correct](https://xkcd.com/1179/) way to write numeric dates is `YYYY-MM-DD`,
(i.e. ISO 8601).

Good names:

```text
2017-08-01_results/
2016-04-22_meeting_notes.txt
2018-11-29_raw-data-from-john-doe.tar.gz
```

## Lowercase and uppercase

Using purely lowecase letters, or a mixture of lower and uppercase letters
in filenames are both ok. It's a matter of personal preference.

Avoid having files that differ only by case in the same directory. e.g.

```text
notes.txt
Notes.txt
```

