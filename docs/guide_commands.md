![Screenshot](img/slim/guide_logo4.png) 

# Commands 

## Main Pipeline 

A pipeline implementin the BridgePRS method desribed in our Nature
Genetics paper can be run with the following command:

    bridgePRS pipeline go


Which is typically run using two [population configuration files](guide_input.md#config-files) and information about population distance and phenotype: 

    bridgePRS pipeline go -o out --config_files BASE.config TARGET.config --phenotype height --fst 0.1 

To confirm that the population config files and options requested are compatible and properly formatted, the 
following command can be used before running bridgePRS. 
    
    bridgePRS pipeline check

The BridgePRS pipeline command consists of multiple related subprograms that 
correspond to the Stage 1 and Stage 2 analyses described in our [guide](guide_background.md) 
and shown in Figure 1 in our [Nature Genetics Paper](https://www.nature.com/articles/s41588-023-01583-9). 
BridgePRS runs these programs serially and produces [output](guide_output.md) for each model type in the following folders: 

1. **out/prs-single_TARGET** Model 1 (single population) results.  
2. **out/prs-prior_TARGET-BASE** Model 2 (informed prior from base pop) result. 
3. **out/prs-combined_TARGET-BASE** The Model 3 (M1+M2) result and a final weighted result. 


## Pipeline Subprograms 

Each of pipeline subprograms can be run separately using the following commands: 





### prs-single 

Stage 1 analysis to estimate model M1 in the target population can be carried as a standalone 
single population analysis or as part of the larger pipeline where it is used to capture target 
population specific effects:  


    bridgePRS prs-single run -o out --config_file TARGET.config --phenotype height 


This subprogram will produce a result file (out/prs-single_TARGET/bridge.target.prs-single.result) that can be 
used for later analysis. 




### build-model

Stage 1 analysis in the base population for input into Stage 2: 

    bridgePRS build-model run -o out --config_file BASE.config --phenotype height 

This subprogram will produce a model result file (out/build-model_BASE/bridge.base.build-model.result) that 
can be used in the next step. 



### prs-prior 

Stage 2 analysis to estimate the informed model M2 for the target population: 

    bridgePRS prs-prior run -o out --model_file out/build-model_BASE/brige.base.build-model.result  --config_file TARGET.config --phenotype height 
  
This subprogram will produce a result file (out/prs-prior_TARGET-BASE/bridge.target-base.prs-prior.result) that can be 
used for later analysis. 

### analyse 

The Stage 1 and Stage 2 analysis can be analyzed and combined with the following command: 

    bridgePRS analyze combine -o out --result_files  out/prs-single_TARGET/bridge.target.prs-single.result out/prs-prior_TARGET-BASE/bridge.target-base.prs-prior.result

This subprogram will produce result files and plots (by default) in the directory out/prs-combine_TARGET_BASE. 


### prs-port 

Optionally, if gwas summary statistics are not available for the target population, the results from the base population can be ported directly to estimate 
the target GWAS.  

    bridgePRS prs-port run -o out --model_file out/build-model_BASE/brige.base.build-model.result  --config_file TARGET.config --phenotype height 

To run this step in the pipeline the flag --port can be added. 



## Axillary Tools


BridgePRS contains a suite of tools that can be used to reformat files, create config files, and validate file types.  These 
programs can be called using the command: 

    bridgePRS tools  


### check-requirements 

To check if your system settings are compatible with bridgePRS, please type the command: 

    bridgePRS tools check-requirements 

### check-pop

To validate inputs and create a single population configuration file, a command similar to the following can be run: 

    bridgePRS tools check-pop --sumstats_prefix TARGET.SUMSTATS.txt --genotype_prefix TARGET_GENOTYPES.txt --phenotype_file TARGET_PHENOTYPES.txt --sumstats_size 100000  

This program will produce a new config file that can be used for this population. 

### check-pops

To validate inputs for two populations (base and target) and create two population configuration files, a command similar to the following can be run: 

    bridgePRS tools check-pops --sumstats_prefix BASE.SUMsTATS.txt TARGET.SUMSTATS.txt --genotype_prefix BASE_GENOTYPES.txt TARGET_GENOTYPES.txt --phenotype_file TARGET_PHENOTYPES.txt --sumstats_size 100000  

This program will produce two config files for later use. 

### reformat-sumstats

Sumstats files are not standardized and often omit information like ref/alt alleles.  For this reason bridgePRS allows you to reformat a sumstats file using 
genotype data to confirm/add information, using the following command: 

    bridgePRS tools reformat-sumstats --sumstats_prefix TARGET.SUMSTATS.txt --genotype_prefix TARGET_GENOTYPES.txt 

This program will produce a new sumstats file for this population. 

