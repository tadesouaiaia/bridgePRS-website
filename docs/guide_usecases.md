![Screenshot](img/slim/guide_logo3.png)


## Training

In the two [toy-data examples](quikstart_demo.md) the target
population was African (**AFR**) and the base population was European
(**EUR**).  In these examples each population had a corresponding:

- LD reference panel
- GWAS summary statistics file  
- Individual levels genotype data in plink binary format
- Phenotype data 

Here we consider using BridgePRS in other scenarios with less
available data.  In each of these examples the task is to create
valid configuration files given the described scenario.

## Challenge 1: 

I have access to genotype/phenotype data (<1000 samples, continuous
phenotype) from a population in Central Africa (1,2).  I would like ot
run PRS as accurately as possible, but my dataset is not large enough
to conduct GWAS, however, I do have access to a moderately sized
(25,000 samples) GWAS summary statistics from a West African
population (3) and access to summary statistics from a GWAS of a large
(500k) European population (4).  I also have access to the 1000G
reference panels, how can I analyze my data?
 
**Available Data:** 

1. caf/genotypes/caf_genotype.bed, caf_genotype.bim, caf_genotype.fam 
2. caf/phenotypes/caf_test.dat, ukb/phenotypes/caf_validation.dat 
3. yoruba/sumstats/yoruba.chr1.glm.gz,...,yoruba.chr22.glm.gz 
4. ukb/sumstats/ukb.sumstats.gz 
5. 1000G Reference Panel 

Can you fill out the configuration files to carry this out? 

=== "Target Config File"

    ```R
    POP=
    LDPOP=
    LD_PATH=
    SUMSTATS_PREFIX=
    SUMSTATS_SUFFIX=
    SUMSTATS_SIZE=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILE=
    VALIDATION_FILE=
    ```

=== "[Answer]"

    ```R
    POP=CAF
    LDPOP=AFR 
    LD_PATH=data/1000G_SAMPLE
    SUMSTATS_PREFIX=yoruba/sumstats/yoruba.chr 
    SUMSTATS_SUFFIX=.glm.gz 
    SUMSTATS_SIZE=25000
    GENOTYPE_PREFIX=caf/genotypes/caf_genotype 
    PHENOTYPE_FILE=caf/phenotypes/caf_test.dat  
    VALIDATION_FILE=caf/phenotypes/caf_validation.dat 
    ```

=== "Model Config FIle"

    ```R
    POP=
    LDPOP=
    LDPATH= 
    SUMSTATS_FILE=
    SUMSTATS_SUFFIX=
    SUMSTATS_SIZE=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILES=
    ```

=== "Answer"

    ```R
    POP=EUR
    LDPOP=EUR
    LD_PATH=data/1000G_SAMPLE
    SUMSTATS_FILE=ukb/sumstats/ukb.sumstats.gz 
    SUMSTATS_SIZE=500000
    GENOTYPE_PREFIX=caf/genotypes/caf_genotype 
    PHENOTYPE_FILE=caf/phenotypes/caf_test.dat  
    VALIDATION_FILE=caf/phenotypes/caf_validation.dat 
    ```




## Challenge 2: 

I have access to GWAS summary statistics (1) and genotype/phenotype
(2,3) data (>2000 samples, binary phenotype) from a moderate sized
population in Eastern Europe. I have reason to believe that this
population has unique LD structure and would like to incorporate this
into my model. I also have GWAS (4) and genotype/phenotype data from
the UKB biobank (5,6) that I wish to use to improve my results, how
should I do this?

1. ukr/sumstats/ukr.sumstats.out 
2. ukr/genotypes/chr1.bed,bim,fam...chr22.bed,bin,fam, 
3. ukr/phenotypes/ukr_test.dat, ukr/phenotypes/ukr_validation.dat 
4. ukb/sumstats/ukb.sumstats.gz 
5. ukb/genotypes/chr1.bed,bim,fam...chr22.bed,bin,fam
6. ukb/phenotypes/ukb_test.dat, ukb/phenotypes/ukb_validation.dat 




=== "Target Config File"

    ```R
    POP=
    LDPOP=
    LDPATH=
    SUMSTATS_PREFIX=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILE=
    VALIDATION_FILE=
    ```

=== "[Answer]"

    ```R
    POP=ukr
    LDPOP=ukr*
    LDPATH=CUSTOM
    SUMSTATS_PREFIX=ukr/sumstats/ukr.sumstats  
    SUMSTATS_SIZE=2000 
    GENOTYPE_PREFIX=ukr/phenotypes/chr
    PHENOTYPE_FILE=ukr/phenotypes/ukr_test.dat 
    VALIDATION_FILE=ukr/phenotypes/ukr_validation.dat
    ```

=== "Model Config FIle"

    ```R
    POP=
    LDPOP=
    SUMSTATS_PREFIX=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILE=
    VALIDATION_FILE=
    ```

=== "Answer"

    ```R
    POP=UKB
    LDPOP=EUR 
    LDPATH=1000G
    SUMSTATS_PREFIX=ukb/sumstats/ukb.sumstats
    SUMSTATS_SIZE=500000
    GENOTYPE_PREFIX=ukb/genotypes/chr
    PHENOTYPE_FILE=ukb/phenotypes/ukb_test.dat 
    VALIDATION_FILE=ukb/phenotypes/ukb_validation.dat 
    ```




  
















