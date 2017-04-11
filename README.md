# JEPEGMIX2

##Download JEPEGMIX2
The current release (Version 0.1.0) of JEPEGMIX2 is for a Linux user. The pre-compiled executables for other operating systems (e.g.,  Windows, MacOS) will be available soon. The latest source codes of JEPEGMIX2 are available upon request (chris.chatzinakos@vcuhealth.org)

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[JEPEGMIX2 for a Linux user](https://www.dropbox.com/sh/486d12phqs0ozif/AABLNCff1g-8oGi8KucZ2PARa?dl=0)|v0.1.0|04/11/2017|

##Download Reference Panels
|**Direct download link**|**Number of Samples**|**Number of populations**|**NCBI build**|**Release Date**|**Note**|
|:---|:---|:---|:---|:---|:---|
|[1000 Genomes Phase1 Release3](https://www.dropbox.com/sh/a0ycbgi6fhdcasw/AAAnM0CmUl7nXkOumKv6QNiOa?dl=0)|1092|14|build 37 (hg19)|Nov. 23 2010|Includes chr1-chr22|

Here are the 1000 Genome population abbreviations used by JEPEGMIX2. AFR is an abbreviation for African; AMR for admixed American; ASN for East Asian; EUR for European. 

|**Population Abbreviation**|**Number of Subjects**|**Super Population**|**Population Description**|
|:---|:---|:---|:---|
|ASW|61|AFR|African Ancestry in Southwest US|
|CEU|85|EUR|Utah residents (CEPH) with Northern and Western European ancestry|
|CHB|97|ASN|Han Chinese in Beijing, China|
|CHS|100|ASN|Southern Han Chinese|
|CLM|60|AMR|Colombian in Medellin, Colombia|
|FIN|93|EUR|Finnish in Finland|
|GBR|89|EUR|British in England and Scotlant|
|IBS|14|EUR|Iberian populations in Spain|
|JPT|89|ASN|Japanese in Tokyo, Japan|
|LWK|97|AFR|Luhya in Wenbuye, Kenya|
|MXL|66|AMR|Mexican Ancestry from Los Angeles, USA|
|PUR|55|AMR|Puerto Rican in Puerto Rico|
|TSI|98|EUR|Toscani in Italia|
|YRI|88|AFR|Yoruba in Ibadan, Nigeria|

##Download SNP Annotation Data

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[SNP annotations](https://www.dropbox.com/sh/ydbwhq2hixtoqjk/AABACP9w17i--gWLGQHNtesea?dl=0)|v0.2.0|11/20/2014|

##JEPEGMIX2 Input File Format

###JEPEGMIX2 takes as input a plain text file with rows and columns denoting SNPs and variables, respectively. The first line of the input file should be column names/headers. Data entries on each line should be separated by white space. 
The file should contain six columns, and optional another one: 1) rsid (SNP ID), 2) chr (chromosome number), 3) bp (base pair position), 4) a1 (reference allele), 5) a2 (alternative allele), 6) z (normally distributed GWAS/meta-analysis summary statistic, i.e. two-tailed Z-score) and 7) info (imputation information)). JEPEGMIX2 does not require the input data to be sorted in ascending order by chromosome number and base pair position or SNP ID. Here is a sample JEPEGMIX2 input file.

```
rsid        chr  bp         a1  a2  z          info    

rs1000109   9    117908733  C   T  -0.714464   0.890   

rs10001109  4    44904653   C   T   0.721919   0.731   

rs1000112   22   28273339   C   G  -0.583666   0.445 

rs10001127  4    130547376  T   C   0.069329   0.999    

rs1000113   5    150240076  T   C  -1.447288   1.0  
```

**DISTMIX2 (version.0.1.0) imputation:** If your input summary data is generated from non-imputed genotype data (i.e. non-imputed GWASs or exome sequencing studies), you may want to impute summary statistics of unmeasured functional variants based on external panels (e.g. 1000 Genomes). By using "--impute" option, you can make the software impute them using DISTMIX2 before performing JEPEGMIX2 analysis. In this case, the software assumes that all SNPs in your input file are measured and does not use the imputation information provided in the "info" column (if this column exist in your input file).

**Note:** If the input summary data comes a different genome assembly (e.g. NCBI build 36 (hg18)) than NCBI build 37 (hg19), it needs to be converted by the user to NCBI build 37 (hg19) using a software, called [liftover](https://genome.ucsc.edu/cgi-bin/hgLiftOver), from UCSC.


Here is a sample JEPEGMIX2 population weight file. 

```
pop	wgt   

ASW	0.1

GBR	0.3

FIN     0.2

CEU	0.25

IBS	0.15
```

The first line of the population weight file should be column names/headers. The file should contain two columns: 1) pop (population abbreviation) and 2) wgt (population proportion). The columns of data should be separated by white space. The weight file name should be specified with the ‘--populationWeight’ option.
   
##JEPEGMIX2 output file format

The JEPEGMIX2 output file has fourteen columns: 1) type name (Type), 2) tissue name (Tissue), 3) gene name (Geneid), 4) chromosome (Chr), 5) bare paise start (bp_s), 6) bare paise end (bp_e), 7) number of functional SNPs associated with gene (Num_SNPs), 8) pre sestimated q value (Q), 9) JEPEGMIX2 z-value for non centrality case (Zval) 10) JEPEGMIX2 p-value for non centrality case (Pval) 11) JEPEGMIX2 q-value for non centrality case (Qval), 12) JEPEGMIX2 z-value for centrality case (Zval_c) 13) JEPEGMIX2 p-value for centrality case (Pval_c), 14) JEPEGMIX2 q-value for centrality case (Qval_c). The first line of the output file is column names/headers.  Here is a sample JEPEGMIX2 output file, with 3 genes:

```
Type          Tissue              Geneid    Chr   bp_s      bp_e    Num_SNPs    Q       Zval      Pval     Qval   Zval_c    Pval_c   Qval_c

Gene   TW_Artery_Coronary_0.5      FABP3    1   30852689   32699227   76   0.0127005   1.85878   0.0630578   1   1.85878     0.0630578  1

Gene   TW_Artery_Coronary_0.5      TXLNA    1   32480657   32480657   1    0.00194273  -1.72314   0.0848635  1   -1.72314    0.0848635  1

Gene   TW_Artery_Coronary_0.5      DCDC2B   1   32160918   33610468   11   0.0205775    0.996671  0.318924   1   0.996671    0.318924   1

```

**Note:** If there are no functional SNPs for genes the results will be NA and the will print at the begin of the output file.


##Options

|**Option**|**Short Flag**|**Parameter**|**Default**|**Description**|
|:---|:---|:---|:---|:---|
|--version|-v|none|none|Prints version information.|
|--help|-h|none|none|Outputs a full description of all JEPEGMIX2 options.|
|--impute|none|none|none|Imputes summary statistics of unmeasured functional SNPs using DISTMIX2 before JEPEGMIX2 analysis.|
|--reference|-r|filename|none|The filename of the reference population data.|
|--referenceIndex|-i|filename|none|The filename of the reference population index data.|
|--annotation|-a|filename|none|The filename of the SNP annotation data set.|
|--output|-o|filename|out.jepegmix|The filename of JEPEGMIX2 output|
|--windowSize|-n|decimal|1.0|The size of the DISTMIX prediction window (Mb).|
|--wingSize|-m|decimal|0.5|The size of the wing padded on the left and right of the DISTMIX prediction window (Mb).|
|--populationWeight|-w|filename|none|The filename of the population weight data.|
|--rmv|none|none|none|Rare variant weights.|

