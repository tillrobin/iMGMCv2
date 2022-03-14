# iMGMC - integrated Mouse Gut Metagenomic Catalog v2

![logo](/images/logo.png)

```diff
- preview for alpha test (so far only for internal use, updates will follow)
```

## Description
*Creation of an updated mouse gut gene catalog*
  - ~200K MAGs representing 3k species
  - more diverse samples from new studies (~10) and public studies (~80)
  - integrated isolated species
  - improved pipelines

## Data

### Metagenome-assembled genomes (MAGs) :

| Description | Size | Link |
|--|--|--|
| representative mMAGs (n=3,###) | # GB | [iMGMCv2-mMAGs-dereplicated_genomes.tar.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD) | 
| representative hqMAGs (n=2,###) | # GB | [iMGMCv2-hqMAGs-dereplicated_genomes.tar.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD) | 
| all mMAGs (n=###,###) | ## GB | [iMGMCv2-mMAGs.tar.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD)| 
| Annotations by CheckM, dRep-Clustering, GTDB-Tk | # MB | [MAG-annotation_CheckM_dRep_GTDB-Tk.tar.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD) |
| Functional annotations (hqMAGs by eggNOG mapper v2) | ### MB | [hqMAGs.emapper.annotations.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD) |
| preprocess mapping-index | ## GB | [hqMAGs.emapper.annotations.gz](https://nubes.helmholtz-berlin.de/s/dbpSFs97NTbfJbD) |

## Pipilines

### Genome based abundance profilling

download index, TPM-Script, summarizing script
load bioconda, run mapping
pipeup sam-file, norm to TPM, sumup for all samples, plot data


See our paper for details.

**An integrated metagenome catalog enables new insights into the murine gut microbiome**  
Till R. Lesker, Abilash C. Durairaj, Eric. J.C. Gálvez, Ilias Lagkouvardos, John F. Baines, Thomas Clavel, Alexander Sczyrba, Alice C. McHardy, Till Strowig. *Cell reports* 30, no. 9 (2020): 2909-2922.
https://doi.org/10.1016/j.celrep.2020.02.036
 