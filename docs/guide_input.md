![Screenshot](img/slim/guide_logo2.png) 
# Input Data


## The LD Reference Panel  

BridgePRS requires representative genotype data in PLINK binary (bed)
format to estimate LD.  A thinned LD reference panel (19734 SNPs)
for use with the [quick start tutorial](quikstart_data.md) is included 
in the BridgePRS download (**data/1000G_sample**). Three full-size 1000 Genomes panels 
covering **AFR**, **EUR**, **EAS**, **SAS**, and **AMR** super-populations with 
different SNP sets are available for download: 
(1) [All HapMap Variants](https://drive.google.com/file/d/1D0ZtPrvkvznKfHjlwo6BkYIvWFIRF_9g/view?usp=drive_link),(2) [All 1000G variants with MAF>5% in any of the five 1000G super-populations](https://drive.google.com/file/d/1c3BamSz1JpXr0QQIfyI_1nUfe0SRNXKa/view?usp=drive_link),(3) [All 1000G variants with MAF>1% in any of the five 1000G super-populations](https://drive.google.com/file/d/18xgsyDymbjeSOv1QS2ULQFaru5NVjwGR/view?usp=drive_link).


To run bridgePRS using a custom LD reference panel see [customisation](guide_customization.md).

## Config Files: Target/Base Population Data: 


For the target and base populations BridgePRS requires inputs be supplied in population configuration files.  The following arguments are required in the target configuration file: 

|Variable Name|Notes|
|:--|:--|
|POP                 | Population name label, eg. AFR | 
|LDPOP               | Name of 1000G population used to estimate LD (AFR, AMR, EAS, EAS, SAS) | 
|LD_PATH             | Path to LD reference data | 
|SUMSTATS_FILE       | Sumstats filename used for genomewide summary statistics | 
|SUMSTATS_PREFIX     | Sumstats prefix used for summary statistics split by chr, eg. `height_chr`|
|SUMSTATS_SUFFIX     | sumstats suffix, eg `.txt.gz`, gives sumstats files `height_chr1.txt.gz -- height_chr22.txt.gz` |
|SUMSTATS_SIZE       | GWAS sample size (required for multi-ancestry)| 
|GENOTYPE_PREFIX     | Path and prefix to plink bed files of test and validation samples | 
|PHENOTYPE_FILE      | File of phenotype and covariate of test data | 

The following optional inputs can also be supplied: 

|Variable Name|Notes|
|:--|:--|
| VALIDATION_FILE  | File of phenotype and covariate of validation data |
| SNP_FILE       | File listing SNP ids to use in analysis, eg. QCed SNPs | 
| MAX_CLUMP_SIZE| Maximum number of SNPs per clump  | 
| COVARIATES | List of covariates (comma separated) to use, eg: COVARIATES=PC1,PC2,PC3| 

Sumstats format is not standardized, bridgePRS requires text files
with at least five columns the denote the snp-id (rsid), reference
allele, alternate allele, p-value, and weight (beta or log odds).  The
file specifc
column headers can be supplied as an ordered 5mer (a) or on individual lines in the sumstats file:  

|Variable Name|Description|
|:--|:--|
|SUMSTATS_FIELDS   | DEFAULT: SUMSTATS_FIELDS=ID,REF,A1,P,BETA| 
|SSF-SNPID   | Column name of SNP ID (default ID) | 
|SSF-REF    | Column name of Ref Base (default REF)|
|SSF-ALT    | Column name of Alt Base (default ALT)|
|SSF-P    | Column name of Pvalue (default P| 
|SSF-BETA   | Sumstats Field Name for Beta (default BETA| 

<!--
|Input|Variable Name|Example|
|:-:|:-:|:-:|
|Sumstats Fields    |SUMSTATS_FIELDS   | DEFAULT: SUMSTATS_FIELDS=ID,REF,A1,P,BETA| 
|b1) SNP Field     |SSF-SNPID   | Sumstats Field Name for SNP-ID | 
|b2) Field     |SSF-REF    | Sumstats Field Name for Ref Base |
|b3) Alt Field     |SSF-ALT    | Sumstats Field Name for Alt Base |
|b4) Pval Field     |SSF-P    | Sumstats Field Name for Pvalue | 
|b5) Beta Field     |SSF-BETA   | Sumstats Field Name for Beta | 
-->

---


## Creating a Config File: 


!!! tip "Creating a Configuration File"
    The following command will validate the command line data and create a target configuration file 
    ```
    ./bridgePRS tools check-pop -o test --pop AFR --ld_path ./data/1000G_sample/ --sumstats_prefix ./data/pop_AFR/sumstats/AFR.chr 
                                                                                     --sumstats_size   10000
                                                                                     --genotype_prefix ./data/pop_AFR/genotypes/chr 
                                                                                     --phenotype_file ./data/pop_AFR/phenotypes/AFR_test.dat


    ```
    To create a target and base configuation file you can use the following command: 
    ```
    ./bridgePRS tools check-pops -o test --pop AFR EUR --ld_path ./data/1000G_sample/ --sumstats_prefix ./data/pop_AFR/sumstats/AFR.chr ./data/pop_EUR/sumstats/EUR.chr 
                                                                                     --sumstats_size   10000 100000 
                                                                                     --genotype_prefix ./data/pop_AFR/genotypes/chr 
                                                                                     --phenotype_file ./data/pop_AFR/phenotypes/AFR_test.dat



    ```
    

This command will create target and base configuration files can be observed below: 



## Config Files: Target/Base Population Data: 

=== "cat test/save/target.AFR.config"

    ```R
    POP=AFR
    LDPOP=AFR
    LD_PATH=$BRIDGEDIR/data/1000G_sample
    SUMSTATS_PREFIX=test/save/sumstats/ss.AFR.
    SUMSTATS_SUFFIX=.out.gz
    SUMSTATS_FIELDS=ID,REF,A1,P,BETA
    SUMSTATS_SIZE=10000
    SNP_FILE=test/save/snps.afr_valid.txt
    GENOTYPE_PREFIX=$BRIDGEDIR/data/pop_AFR/genotypes/chr
    PHENOTYPE_FILE=tests/save/AFR.test_phenos.dat
    VALIDATION_FILE=test/save/AFR.valid_phenos.dat
    ```

=== "cat out/save/base.EUR.config" 

    ```R

    POP=EUR
    LDPOP=EUR
    LD_PATH=$BRIDGEDIR/data/1000G_sample
    SUMSTATS_PREFIX=test/save/sumstats/ss.EUR.
    SUMSTATS_SUFFIX=.out.gz
    SUMSTATS_FIELDS=ID,REF,A1,P,BETA
    SUMSTATS_SIZE=100000
    SNP_FILE=test/save/snps.afr_valid.txt
    GENOTYPE_PREFIX=$BRIDGEDIR/data/pop_AFR/genotypes/chr
    PHENOTYPE_FILE=$BRIDGEDIR/data/pop_AFR/phenotypes/AFR_test.dat
    ```

---

## File Specifications 


### 1) Sumstats Data 

GWAS summary statistics are provided using a prefix to one or many (per chromosome) files with the `--sumstats_prefix` argument and the 
`--sumstats_suffix` argument when nevecessary.  GWAS summary statistics must be provided as a whitespace delimited file containing 
the results of an association study for a given phenotype.  BridgePRS has no problem reading in a gzipped base file 
(need to have a **.gz** suffix) or splitting the file by chromosome if necessary.  An example of a sumstats file with default column headers is shown: 


Defaults|#CHR|ID|REF|A1|P|BETA|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
Variable||--ssf-snpid|--ssf-ref|--ssf-alt|--ssf-beta|--ssf-p|
Data|1|rs121|T|G|0.0413692|0.9472871|
Data|1|rs497|C|A|0.328347|-1.193074|
Data|1|rs271|G|G|0.0132225|0.413687|

The **--ssf** arguments can be used to specify column headers for different files. 






### 2) Genotype Files

Genotype files must be in Plink Format.  

### 3) Phenotype Files
Phenotype files can be provided to BridgePRS using the `--phenotype_files` flag. 
This must be a tab / space delimited file and missing data **must** be represented by either `NA` or `-9` (only for binary traits).
The first two column of the phenotype file should be the FID and the IID, and the rest can be phenotypes/covariates:  

|FID|IID|y|y.binary|PC1|PC2|
|:-:|:-:|:-:|:-:|:-:|:-:| 
|afr1_1|afr2_1|24.4|1|0.53|0.950| 
|afr1_2|afr2_2|4.10|0|0.59|0.450| 
|afr1_3|afr2_3|37.2|1|0.73|-0.13| 
|afr1_4|afr2_4|5.40|0|0.44|-0.55| 


The phenotype of interest can be specified with the `--phenotype` flag and the covariates can be given as a comma separated list 
after the `--covariates` flag: 



### 4) QC SNP List 
To select only SNPS that have passed QC, you can include a single column text file using the  `--snp_file` flag. 





