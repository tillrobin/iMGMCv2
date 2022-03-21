# iMGMC - integrated Mouse Gut Metagenomic Catalog v2

![logo](/images/logo.png)

```diff
- preview for alpha test (so far only for internal use, updates will follow)
```

## Description
*Creation of an updated mouse gut gene catalog*
  - MAGs representing n species
  - more diverse samples from new studies (~n) and public studies (~n)
  - integrated isolated species
  - improved pipelines

## Data

### Metagenome-assembled genomes (MAGs) :

```diff
- The data is still protected at the moment, we will change this as soon as possible.
```

| Description | Size | Link |
|--|--|--|
| representative mMAGs (n=#,###) | # GB | [iMGMCv2-mMAGs-dereplicated_genomes.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) | 
| representative hqMAGs (n=#,###) | # GB | [iMGMCv2-hqMAGs-dereplicated_genomes.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) | 
| all mMAGs (n=###,###) | ## GB | [iMGMCv2-mMAGs.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA)| 
| Annotations by CheckM, dRep-Clustering, GTDB-Tk | # MB | [MAG-annotation_CheckM_dRep_GTDB-Tk.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |
| Functional annotations (hqMAGs by eggNOG mapper v2) | ### MB | [hqMAGs.emapper.annotations.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |
| preprocess mapping-index | ## GB | [hqMAGs.emapper.annotations.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |

# Pipelines

## Genome based abundance profilling

### 1. We recommend the use of [Bioconda](http://bioconda.github.io/) eg create bioconda environment with bwa2 and bbmap with:

    conda create -n iMGMCv2 bwa2 bbmap
	conda activate iMGMCv2

## 2. Download or create bwa2 index form iMGMCv2-DU6-mMAGs.fasta

### 2a. Download bwa2-index (Warning 25,7GB but you can use option 2b as an alternative)

    download [iMGMCv2-DU6.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) 
	tar -xzf iMGMCv2-DU6.tar.gz

### 2b. Download mMAG-fasta and run bwa2-index (700 MB, will take some hours to process)

    download [iMGMCv2-DU6-mMAGs.fasta.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) 
	gzip -d iMGMCv2-DU6-mMAGs.fasta.gz
	bwa-mem2 index iMGMCv2-DU6-mMAGs.fasta

## 3. Map the samples with bwa2 to the iMGMCv2-DU6-mMAGs.fasta

	Cores=24                      # please check your server
	RefFasta=DU6.fasta            # bwa2 index
	FastqPathR1=/path/to/file/R1  # set path to read 1
	FastqPathR2=/path/to/file/R2  # set path to read 2
	SampleName=MySampleName       # create name for the samples

### 3a. Mapping to sam-file and sumup via pipeup from bbmap-tools (create sam-file I/O-weighted)

    bwa-mem2 mem -t ${Cores} ${RefFasta} ${FastqPathR1} ${FastqPathR2} | pigz --fast > /tmp/${SampleName}.sam.gz
	pileup.sh in=/tmp/${SampleName}.sam.gz covstats=${SampleName}.covstats 32bit=t 2> ${SampleName}.log
	rm /tmp/${SampleName}.sam.gz

### 3b. Mapping and pipe direct to pipeup (need more memory ~100GB insteat of 60GB, about 10% faster)

    bwa-mem2 mem -t ${Cores} ${RefFasta} ${FastqPathR1} ${FastqPathR2} | \
	pileup.sh in=stdin.sam covstats=${SampleName}.covstats 32bit=t 2> ${SampleName}.log

## 4. Convert covstats to TPM (normalize count data to genome size and relative to 1 million reads)

    bash TPM-Script ${SampleName}.covstats # create TPM-${SampleName}.txt
	bash create-abundance-table.sh         # summarizing all Samples into one matrix file

## 5. [Optimal] join abundance-table with more samples

We are using a close reference profiling, so we can join other samples to the abundance-table. This make it easy to analyze your samples in a bigger context.

	YourTable=abundance-table.txt              # table form step before
	OtherTable=other-abundance-table.txt       # another table
	SampleList=RefSamplesMircobiotas.txt       # File with names of samples you want to join (alternative all)

    bash add-samples.sh ${YourTable} ${RunTable} ${SampleList} # add selected samples
	bash add-samples.sh ${YourTable} ${RunTable}               # add all samples

## 6. Plot data

First create a mapping files with all needed samples and the metadata (like a simple group):

Sample	Factor
Trt1	Treatment
Trt2	Treatment
Trt3	Treatment
Con1	Control
Con2	Control
Con3	Control


This data can used for downstream processing like ploting in R:


See our paper for details.

**An integrated metagenome catalog enables new insights into the murine gut microbiome**  
Till R. Lesker, Abilash C. Durairaj, Eric. J.C. Gálvez, Ilias Lagkouvardos, John F. Baines, Thomas Clavel, Alexander Sczyrba, Alice C. McHardy, Till Strowig. *Cell reports* 30, no. 9 (2020): 2909-2922.
https://doi.org/10.1016/j.celrep.2020.02.036
 