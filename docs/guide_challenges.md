![Screenshot](img/slim/guide_logo3.png)


## Training

In the two [toy-data examples](quikstart_data.md) the target population was a non-specific African (**AFR**) population 
and the model population  was European (**EUR**).  In these examples each population had a corresponding:  

- LD Reference Panel (Used for Clumping) 
- GWAS Summary Stat File  
- Genotype/Phenotype Data 

This example may be unrealistic given real-world constraints and the realities of data sharing. 
Here we will consider will consider using BridgePRS in more realistic scenarios.  In each of these 
challeges the task is to create valid configuration given the described scenario. 

## Challenge 1: 

**I have access to genotype/phenotype data (<1000 samples, continuous phenotype) from a diverse population in Central Africa (1,2). 
I would like ot run PRS as accurately as possible, but my dataset is not large enough to conduct GWAS, however, I do have access to a moderately 
sized GWAS in a related West African population (3) and access to large-scale GWAS data from a European population (4).  I also have 
access to the 1000G reference panels, how can I analyze my data?**
 
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
    SUMSTATS_PREFIX=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILE=
    VALIDATION_FILE=
    ```

=== "[Answer]"

    ```R
    POP=CAF
    LDPOP=AFR 
    SUMSTATS_PREFIX=yoruba/sumstats/yoruba.chr 
    SUMSTATS_SUFFIX=.glm.gz 
    GENOTYPE_PREFIX=caf/genotypes/caf_genotype 
    PHENOTYPE_FILE=caf/phenotypes/caf_test.dat  
    VALIDATION_FILE=caf/phenotypes/caf_validation.dat 
    ```

=== "Model Config FIle"

    ```R
    POP=
    LDPOP= 
    SUMSTATS_PREFIX=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILES=
    ```

=== "Answer"

    ```R
    POP=EUR
    LDPOP=EUR
    SUMSTATS_PREFIX=ukb/sumstats/ukb.sumstats
    GENOTYPE_PREFIX=caf/genotypes/caf_genotype 
    PHENOTYPE_FILE=caf/phenotypes/caf_test.dat  
    VALIDATION_FILE=caf/phenotypes/caf_validation.dat 
    ```




## Challenge 2: 

**I have access to GWAS data (1) and  genotype/phenotype (2,3) data (>2000 samples, binary phenotype) from a moderate sized population in Eastern Europe. 
I have reason to believe that this population has unique LD structure and would like to incorporate this into my model.  
I also have GWAS (4) and genotype/phenotype data from the UKB biobank (5,6) that I wish to use to improve my results, how should I do this? 

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
    SUMSTATS_PREFIX=
    GENOTYPE_PREFIX=
    PHENOTYPE_FILE=
    VALIDATION_FILE=
    ```

=== "[Answer]"

    ```R
    POP=ukr
    LDPOP=ukr*
    SUMSTATS_PREFIX=ukr/sumstats/ukr.sumstats  
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
    SUMSTATS_PREFIX=ukb/sumstats/ukb.sumstats
    GENOTYPE_PREFIX=ukb/genotypes/chr
    PHENOTYPE_FILE=ukb/phenotypes/ukb_test.dat 
    VALIDATION_FILE=ukb/phenotypes/ukb_validation.dat 
    ```




  
















