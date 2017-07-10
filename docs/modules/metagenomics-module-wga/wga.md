#Whole Genome Analysis

##Key Learning Outcomes
---------------------

After completing this module the trainee should be able to:

-   Understand the main approaches to perform metagenomics assembly

-   Be able to perform assembly on your data and assess the quality of your assembly

##Resources You’ll be Using
-------------------------

### Tools Used

Spades.py : http://bioinf.spbau.ru/en/spades3.7  

##Introduction
---

Performing genomic assembly aims at generating a genome-length sequence
using the sequence information obtained from short reads. In the case of
metagenomics sample, the task is complicated by the number of different
genomes present in the sample and the fact that their sequences are
sometimes very similar to each other. There are two main approaches to
perform de novo assembly (genomic or metagenomic): building a consensus
and generating De Bruijn k-mer graph.

###WGS Assembly and Annotation prac
---

The A7A dataset is quite small by metagenomic standards, only about 52M reads, and from a simple and somewhat extreme environment. We have submitted A7A to the EBI Metagenomics pipeline (https://protect-au.mimecast.com/s/ZXg4BMh0dVnRtZ?domain=ebi.ac.uk), and in this pract session you will do some of the preparatory work for the later session where you will compare the results of any assembly-based approach to those that come from the EBI pipeline.

Even though A7A is relatively small, assembling the reads took about an hour with 16 cores and about 20GB of memory - a much more computational task than we could expect you to be able to perform with the resources and time available in this workshop. We have already assembled A7A using metaSpades, and you'll find the assembled contigs and the log from the assembly in /data/A7A_WGS/Spades_A7A.zip. 

The command used for the assembly was: 

```bash
https://protect-au.mimecast.com/s/m4kKB2U1XWe4hD?domain=metaspades.py -o spades --pe1-1 DL3_GATCAG_L008_R1_001.fastq --pe1-2 DL3_GATCAG_L008_R2_001.fastq -m 64	
```
	
You will find that Spades has produced two FASTA files as a result of assembling the reads: contigs.fasta and scaffolds.fasta.

!!! note "What is the difference between these two files? Which one would you use for the next steps of the process?"
    Scaffolds.fasta contains some contigs are made up from two or more smaller contigs together with strings of NNNNNNNs. These are places where the assembler knows that the smaller contigs belong together but cannot fill in the small gap between them. Generally you want to work with contigs.fasta to avoid the runs of NNNNNNNs.

Your next step is to find and annotate the genes in these contigs, and we will use Prokka (https://protect-au.mimecast.com/s/krZGBwfrLKV3UW?domain=vicbioinformatics.com) from Torsten Seeman at the Victorian Bioinformatics Consortium. Your next task is to run Prokka over the contigs.fasta file, getting it to find ORFs and their best matches in the UniProtKB protein database. Prokka is already installed on your prac systems.

```bash
prokka --outdir A7A_prokka --prefix A7A contigs.fasta
```	
Once Prokka has completed, look in the A7A_prokka directory and you will find the results files. For now, we will look at the GenBank format file (.gbk) and the summary table (.tbl).

The /data/A7A directory also contains a number of files from the taxonomic analysis of the A7A dataset, including an OTU table (and OTU sequences) coming from a targeted assembly using the EMB 16S primers; the results of finding and classifying likely 16S reads from the dataset, and these classifications summarised at various tasonomic levels; and the results of using kMer matches to assign a family or genus name to each contig. We will discuss these results, and the results of your Prokka runs in the next prac session, after an introduction to the EBI Metagenomics portal and the results it produces.

