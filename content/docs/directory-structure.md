---
title: Directory Structure
author: Jessica Chung
date: '2017-08-08'
slug: directory-structure
categories: []
tags: []
description: ''
---

When using PEARG clusters or the Melbourne Bioinformatics clusters, your 
files and data should be organised according to the convention described 
here.

Each project should have its own directory located inside your home directory
or a shared location. Your project directory name should be meaningful.

Any shared data such as reference genomes and indices should be stored outside
your project directory to avoid duplication of data.

`TODO: format below into a div`

At minimum, please check:

- is your project name sensible?
- do you have a README file (or equivalent) in the parent directory of your project directory that contains meaningful information?
- do you have a data directory and a results directory?

If you've answered any questions no, you may get a stern email in the future.

## Creating a project directory using the template

`TODO: Create a project skeleton in the future`

## Example directory structure

In this example, our project name is called `project_name` and is a RAD-seq
experiment that was processed using stacks.

```text
project_name/
├── data/
├── results/
├── scripts/
├── software/
└── README
```

The directory has four subdirectories: `data`, `results`, `scripts`, and 
`software`, and one `README` file. The `README` file should be a plain-text
file containing basic project information (e.g. what the project is about, 
what type of data was sequenced).

### Data directory

The `data` directory should contain the raw data received from sequencing.
Each library should have it's own directory containing sequencing files and
a text file containing barcodes corresponding needed for Stacks `process_radtags`.

```text
project_name/
├── data/
|   ├── library_1_raw_data/
|   |   ├── seqA_R1_001.fastq.gz
|   |   ├── seqA_R2_001.fastq.gz
│   │   └──  library_1_barcodes.txt
|   ├── library_2_raw_data/
|   |   ├── seqB_R1_001.fastq.gz
|   |   ├── seqB_R2_001.fastq.gz
│   │   └── library_2_barcodes.txt
├── results/
├── scripts/
├── software/
└── README
```

The files in your data directory should be immutable and should not be edited.

### Results directory

The `results` directory should have one directory for each time you generate
a set of results. Using subdirectories inside the main `results` directory is
recommended because often experiments are re-run in the future (e.g. updated
software versions, more sequencing data, reanalysis before publication). 
I recommend naming the directory with a date in `YYYY-MM-DD` format at the 
beginning of the name so the directories are sorted chronologically.

```text
project_name/
├── data/
├── results/
|   ├── 2017-08-01_results/
|   |   ├── ...
|   |   ├── ...
│   │   └── ...
|   ├── 2017-11-01_extra_samples/
|   |   ├── ...
|   |   ├── ...
│   │   └── ...
|   ├── 2018-05-01_reanalysis/
|   |   ├── ...
|   |   ├── ...
│   │   └── ...
├── scripts/
├── software/
└── README
```

Inside each result subdirectory, there should be multiple directories 
containing output from steps in your workflow.

#### Sequencing data

```text
results/
├── 2017-08-01_results/
|   ├── demuxed_seq/
|   |   ├── mozzie-1.1.fq
|   |   ├── mozzie-1.2.fq
|   |   ├── mozzie-1.rem.1.fq
|   |   ├── mozzie-1.rem.2.fq
|   |   ├── mozzie-2.1.fq
|   |   ├── mozzie-2.2.fq
|   │   └── ...
|   ├── demuxed_cat/
|   |   ├── mozzie-1.fq
|   |   ├── mozzie-2.fq
|   |   ├── mozzie-3.fq
|   │   └── ...
|   └── ...
```

The `demuxed_seq` directory should contain demuxed sequencing data processed by 
`process_ragtags`. Stacks should output four files for each sample listed in
the barcode file. 

`TODO: add trimming step?`

#### Alignment data

```text
results/
├── 2017-08-01_results/
|   ├── demuxed_seq/
|   ├── demuxed_cat/
|   ├── alignments/
|   |   ├── AaegL2/
|   │   │   ├── mozzie-1.AaegL2.sorted.bam
|   │   │   ├── mozzie-1.AaegL2.sorted.bam.bai
|   │   │   ├── mozzie-2.AaegL2.sorted.bam
|   │   │   ├── mozzie-2.AaegL2.sorted.bam.bai
|   │   │   ├── ...
|   │   │   └── AagL2_alignment_code.txt
|   |   ├── AaegL3/
|   │   │   ├── mozzie-1.AaegL3.sorted.bam
|   │   │   ├── mozzie-1.AaegL3.sorted.bam.bai
|   │   │   ├── mozzie-2.AaegL3.sorted.bam
|   │   │   ├── mozzie-2.AaegL3.sorted.bam.bai
|   │   │   ├── ...
|   │   │   └── AagL3_alignment_code.txt
|   └── ...
```

Alignments should be stored in the `alignments` directory with a separate
directory for each reference genome aligned against. Alignments should be stored
as bam files with the `bam` suffix and bam index files, if provided, should end
with `bai`. If alignements are sorted, it's recommended to include `sorted` in
the filename. Including the reference genome name in the filename is also
helpful.

A plain-text file with what commands were run should also be included in the
directory (e.g. `AagL2_alignment_code.txt`) or in the `scripts` directory.

#### Stacks data

```text
results/
├── 2017-08-01_results/
|   ├── demuxed_seq/
|   ├── demuxed_cat/
|   ├── alignments/
|   ├── stacks/
|   |   ├── stacks_AaegL2_females/
|   │   │   ├── ...
|   │   │   ├── ...
|   │   │   ├── stacks_AaegL2_females_populations_filtered_1/
|   |   │   │   ├── ...
|   |   │   │   └── ...
|   │   │   └── stacks_AaegL2_females_populations_filtered_2/
|   |   │   |   └── ...
|   |   ├── stacks_AaegL2_males/
|   |   ├── stacks_AaegL3_females/
|   |   └── stacks_AaegL3_males/
|   └── ...

  
```