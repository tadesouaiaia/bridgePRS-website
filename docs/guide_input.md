![Screenshot](img/slim/guide_logo2.png) 
# Input Data


## LD Reference Panel (--ld_path) 

BridgePRS requires representative genotype data in PLINK binary 
format to estimate LD.  A miniature LD reference panel (**data/1000G_sample**), 
suitable for the [quick start tutorial](quikstart_data.md) is included 
in the BridgePRS download. Three full-size 1000 Genomes panels 
covering **AFR**, **EUR**, **EAS**, **SAS**, and **AMR** super-populations with 
different SNP sets are available for download: (1) [All HapMap Variants](https://drive.google.com/file/d/1EGFap5wjKxIT42SWHKr9MUOzVnK9CVew/view?usp=drive_link),
(2) [All 1000G variants with MAF>5% in any of the five 1000G super-populations](https://drive.google.com/file/d/1rmxKcTGF8XTYU0E7jAIkKsCeedGMNwDE/view?usp=drive_link), 
(3) [All 1000G variants with MAF>1% in any of the five 1000G super-populations](https://drive.google.com/file/d/1RuC8J_qJLDSLnQ4uOGuxx9uGSWg5fxKn/view?usp=drive_link).

If you wish to run bridgePRS using a custom LD reference panel please see [customization](guide_customization.md).

## Target/Base Population Data: 


For the target and base populations BridgePRS requires that the following inputs be supplied 
on the command line or in a configuration file. 
files/names are supplied on the command line or in a configuation file:

|Name|Command Line flag(s)|Description|
|:-:|:-:|:-:|
|Pop Name          |--pop                      |Population Name (Required)|
|LD Pop            |--ldpop                    |LD Reference Population (Required if different from above)|
|LD Panel            |--ld_path                   |Path to LD Reference Panel | 
|(a) Sumstat File  |--sumstats_file            | GWAS Summary Stats (Text Format)|
|(b) Sumstat Filess  |--sumstats_prefix          |GWAS Summary Stats Multiple File(s)|
|Genotype Files |--genotype_prefix                   |Individual Level Genotype Files (Plink Format)|
|Phenotype File |--phenotype_file                    |Individual Level Phenotypes (Text File)|
|Validation File|--validation_file                   |Individual Level Phenotypes for Validation|
|QC-snp List    |--snp_file                          |List QCed SNP ids| 



!!! tip "Creating a Configuration File"
    The following command will validate the command line data and create a target configuration file 
    ```
    ./bridgePRS check pop -o out --pop AFR --sumstats_prefix data/pop_africa/sumstats/afr.chr  
                                           --genotype_prefix data/pop_africa/genotypes/afr_genotypes 
                                           --phenotype_file data/pop_africa/phenotypes/afr_test.dat

    ```
    To create a target and base configuation file you can use the following command: 
    ```
    ./bridgePRS check pops -o out --pop AFR EUR --sumstats_prefix data/pop_africa/sumstats/afr.chr data/pop_europe/sumstats/eur.chr 
                                                --genotype_prefix data/pop_africa/genotypes/afr_genotypes
                                                --phenotype_file data/pop_africa/phenotypes/afr_pheno.dat


    ```
    

This command will create target and base configuration files that can be observed below: 




=== "cat out/save/target.AFR.config"

    ```R
    POP=AFR
    LDPOP=AFR
    SUMSTATS_PREFIX=$BRIDGEDIR/data/pop_africa/sumstats/afr.chr
    SUMSTATS_SUFFIX=.glm.linear.gz
    SNP_FILE=$BRIDGEDIR/out/save/snps.AFR.txt
    GENOTYPE_PREFIX=$BRIDGEDIR/data/pop_africa/genotypes/afr_genotypes
    PHENOTYPE_FILE=$BRIDGEDIR/out/save/AFR.test_phenos.dat
    VALIDATION_FILE=$BRIDGEDIR/out/save/AFR.valid_phenos.dat
    ```

=== "cat out/save/base.EUR.config" 

    ```R
    POP=EUR
    LDPOP=EUR
    SUMSTATS_PREFIX=$BRIDGEDIR/data/pop_europe/sumstats/eur.chr
    SUMSTATS_SUFFIX=.glm.linear.gz
    SNP_FILE=out/save/snps.EUR.txt
    GENOTYPE_PREFIX=$BRIDGEDIR/data/pop_africa/genotypes/afr_genotypes
    PHENOTYPE_FILE=$BRIDGEDIR/data/pop_africa/phenotypes/afr_pheno.dat
    ```




## File Specifications 


### 1) Sumstats Data 

GWAS summary statistics are provided using a prefix to one or many (per chromosome) files with the `--sumstats_prefix` argument and the 
`--sumstats_suffix` argument when nevecessary.  GWAS summary statistics must be provided as a whitespace delimited file containing 
the results of an association study for a given phenotype.  BridgePRS has no problem reading in a gzipped base file 
(need to have a **.gz** suffix) or splitting the file by chromosome if necessary.  An example of a sumstats file with default column headers is shown: 


Default Headers|#CHR|ID|REF|A1|A1_FREQ|OBS_CT|BETA|SE|T_STAT|P|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
Argument||--ssf-snpid|--ssf-ref|--ssf-alt|--ssf-maf|--ssf-n|--ssf-beta|--ssf-se||--ssf-p|
Data|1|rs121|T|G|0.0257573|4853|0.820864|0.413692|1.98424|0.0472871|
Data|1|rs497|C|A|0.483495|4847|0.0011142|0.128347|0.00868116|0.993074|
Data|1|rs271|G|G|0.424387|4814|0.108094|0.132225|0.817497|0.413687|

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

    ```
    ./bridgePRS check data -o out --pop AFR --phenotype y --covariates PC1,PC2 
                           --phenotype_file data/pop_africa/phenotypes/afr_pheno.dat 
    ```

!!! Warning
    The column name(s) should not contain *space* nor *comma*


### 4) QC SNP List 
To select only SNPS that have passed QC, you can include a single column text file using the  `--snp_file` flag. 





