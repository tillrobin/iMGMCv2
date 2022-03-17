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

| Description | Size | Link |
|--|--|--|
| representative mMAGs (n=#,###) | # GB | [iMGMCv2-mMAGs-dereplicated_genomes.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) | 
| representative hqMAGs (n=#,###) | # GB | [iMGMCv2-hqMAGs-dereplicated_genomes.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) | 
| all mMAGs (n=###,###) | ## GB | [iMGMCv2-mMAGs.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA)| 
| Annotations by CheckM, dRep-Clustering, GTDB-Tk | # MB | [MAG-annotation_CheckM_dRep_GTDB-Tk.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |
| Functional annotations (hqMAGs by eggNOG mapper v2) | ### MB | [hqMAGs.emapper.annotations.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |
| preprocess mapping-index | ## GB | [hqMAGs.emapper.annotations.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) |

## Pipilines

### Genome based abundance profilling

**1. We recommend the use of [Bioconda](http://bioconda.github.io/) eg create bioconda environment with bwa2 and bbmap with:

    conda create -n iMGMCv2 bwa2 bbmap
	conda activate iMGMCv2

**2a. Download bwa2-index (Warning 25,7GB but you can use option 2b as an alternative)

    download [iMGMCv2-DU5.tar.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) 
	tar -xzf iMGMCv2-DU5.tar.gz

**2b. Download mMAG-fasta and run bwa2-index (700 MB, like take some hours to process)

    download [iMGMCv2-DU6-mMAGs.fasta.gz](https://1drv.ms/f/s!Am-fED1L6602hcVH65QUhQZse5vOzA) 
	gzip -d iMGMCv2-DU6-mMAGs.fasta.gz
	bwa-mem2 index iMGMCv2-DU6-mMAGs.fasta

**3. Map the samples with bwa2 to the iMGMCv2-DU6-mMAGs.fasta


TPM-Script, summarizing script
load bioconda, run mapping
pipeup sam-file, norm to TPM, sumup for all samples, plot data


See our paper for details.

**An integrated metagenome catalog enables new insights into the murine gut microbiome**  
Till R. Lesker, Abilash C. Durairaj, Eric. J.C. Gálvez, Ilias Lagkouvardos, John F. Baines, Thomas Clavel, Alexander Sczyrba, Alice C. McHardy, Till Strowig. *Cell reports* 30, no. 9 (2020): 2909-2922.
https://doi.org/10.1016/j.celrep.2020.02.036
 