---
title:  "bioinformatics-samtools"
date: 2017-10-31 00:00:00
author: Alain Domissy
tags: 
- ubuntu
- debian
- bioinformatics
- samtools
- bam
- scif
- singularity
files:
 - SingularityApp.samtools
 
---

```yaml
%appinstall bioinformatics-samtools
    apt-get -y install wget
    apt-get -y install autoconf libtool build-essential
    apt-get -y install zlibc libz-dev
    apt-get -y install libncurses5-dev
    apt-get clean
    TARBZ2="samtools-1.3.1.tar.bz2"
    wget https://github.com/samtools/samtools/releases/download/1.3.1/${TARBZ2} -P ./
    tar -C ./ -xjf ./${TARBZ2}
    cd ./samtools-1.3.1
    make && make prefix=../ install
    cd -
    rm ./${TARBZ2}
    rm -rf ./samtools-1.3.1
%appfiles bioinformatics-samtools
%appenv bioinformatics-samtools
    SAMTOOLS_HOME=/scif/apps/bioinformatics-samtools
    export SAMTOOLS_HOME
%apphelp bioinformatics-samtools
    Samtools is a suite of programs for interacting with high-throughput sequencing data. It consists of three separate repositories:
    Samtools: Reading/writing/editing/indexing/viewing SAM/BAM/CRAM format
    BCFtools: Reading/writing BCF2/VCF/gVCF files and calling/filtering/summarising SNP and short indel sequence variants
    HTSlib: A C library for reading/writing high-throughput sequencing data
    It is recommended to create the following alias:
    alias samtools="singularity run --app bioinformatics-samtools \${SINGULARITY_CONTAINER}"
    More help is then available by running
    samtools --help
%apprun bioinformatics-samtools
    samtools "$@"
%applabels bioinformatics-samtools
    MAINTAINER adomissy@ucsd.edu
    BUILD_VERSION 0.0.1
    WRAPPEDTOOL_VERSION 1.3.0
    WRAPPEDTOOL_INFO http://www.htslib.org/
```
