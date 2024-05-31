![Screenshot](img/slim/guide_logo2.png) 
# Input Data


## LD Reference Data: 1000 Genomes 

BridgePRS estimates SNP-specific LD in the clumping step from an population target data in PLINK binary format.  By default, the main 
BridgePRS includes a sample LD reference panel (**BRIDGEDIR/data/1000G_sample**) for population super-groups **AFR** and **EUR** that is 
suitable for the [quick start tutorial](quikstart_data.md). 

A folder containing the full 1000 Genomes LD reference panel for populations **AFR**, **EUR**, **EAS**, **SAS**, and **AMR** can be downloaded 
[here](https://drive.google.com/file/d/1djAEwRiQsh4veinSLHO3laGjNF95vvN9/view?usp=drive_link)
and unzipped into **BRIDGEDIR/data/1000G_ref** to enable full usage of BridgePRS. 

To run BridgePRS using a custom LD reference please see [customization](guide_customization.md). 





## Target/Base Population Data: 


For the target and base populations bridgePRS requires that following files be supplied on the command 
line or in a configuation file: 


|Name|Command Line flag|Target Default|Base Default|Description|
|:-:|:-:|:-:|:-:|:-:|
|Pop Name       |--pop                               |None (Required)       | Required |Target/Base Population Name|
|LD-Ref Pop     |--ld_pop                            |Pop Name              |Pop Name| LD Ref Pop (AFR,EUR,EAS,AMR,SAS) |
|Sumstats       |--sumstats_prefix                   |None (Required)       |Required| GWAS Summary Stats (Text Format)|
|Genotypes      |--genotype_prefix                   |None (Required)       |Target Genotypes| Individual Level Genotypes (Plink Format)|
|Phenotype File |--phenotype_file                    |None (Required)       |Target Phenotypes| Individual Level Phenotypes (Text File)|
|Validation File|--validation_file                   |Half of Phenotype File  |None | Individual Level Phenotypes for Validation|
|QC-snp List    |--snp_file                          |All Snps                |All Snps| List QCed SNP ids| 

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


Default Headers|#CHR|ID|REF|A1|A1_FREQ|OBS_CT|BETA|SE|T_STAT|P|ERRCODE|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
Argument||--ssf-snpid|--ssf-ref|--ssf-alt|--ssf-maf|--sdf-n|--ssf-beta|--ssf-se||--ssf-p|.|
Data|1|rs12184325|T|G|0.0257573|4853|0.820864|0.413692|1.98424|0.0472871|.|
Data|1|rs4970382|C|A|0.483495|4847|0.0011142|0.128347|0.00868116|0.993074|.|
Data|1|rs2710890|G|G|0.424387|4814|0.108094|0.132225|0.817497|0.413687|.|

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





