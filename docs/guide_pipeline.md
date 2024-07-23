![Screenshot](img/slim/guide_logo4.png) 


# Main Program  

A pipeline implementin the BridgePRS method desribed in our Nature
Genetics paper can be run with the following command:

    BridgePRS easyrun go

The pipeline requires the following input from both the target and base populations: 

1. **--pop:** The population name
2. **--ldpop:** The ld reference population, if different from population name
3. **--sumstats_prefix:** Sumstats data 
4. **--genotype_prefix:** Target Genotype Data 
5. **--phenotype_file:** Target Phenotype File 

This information can be provided on the command line or using config
files. The pipeline runs multiple subprograms that are described
below.

# Modelling overview

Figure 1 of our Nature Genetics paper provides an overview of the
modelling implemented by BridgePRS. The BridgePRS pipeline consists
of five related subprograms which correspond to Stage 1 and Stage 2
analyses described in Figure 1. Stage 1 analysis is a single
population analysis. Stage 2 uses the output from a Stage 1 analysis
of the base population as a prior for the target population, this
analysis produces model M1 in Figure 1. Stage 1 analysis of the
target population produces model M2. Model M3 combines PRS from both
Stage 1 and Stage 2 analyses. The final BridgePRS model is a weighted
sum of models M1, M2 and M3.

Model M1 reflects the belief that the target population GWAS is only
informative in conjugtion with the base population GWAS.

Model M2 reflects the belief that the target population GWAS is
informative and the base population GWAS gives no addition
information.

Model M3 reflects the belief both the base and target population GWAS
contribute independent information.

Since apriori we do not know which of the three scenarios
corresponding to models M1, M2 and M3 are true, BridgePRS weights
these models to produce a single target population PRS. However,
BridgePRS reports SNP weights and R2 in the target population for both
the weighted model and M1, M2 and M3 enabling the user to use any of
the four models.

# Subprograms 

1) **BridgePRS prs-single** -- Stage 1 analysis to estimate models M2
and M3
2) **BridgePRS build-model** -- Stage 1 analysis for input into Stage 2
3) **BridgePRS prs-prior** -- Stage 2 analysis to estimate models M1
and M3
4) **BridgePRS analyse combine** -- Estimates models M1, M2, M3 and
weighted model
5) **BridgePRS prs-port** -- Estimates target PRS without target GWAS


##prs-single -- Stage 1 analysis in the NG paper

**prs-single** performs single population analysis. It is used by the
main pipeline to capture target population specific effects.
**prs-single** can be run on its own with the command `./bridgePRS
prs-single run` with the following arguments on the command line or
configuration file:

1. **--pop:** The name of your target population 
2. **--ldpop:** The ld reference name, if different from target population name 
3. **--sumstats_prefix:** Sumstats data 
4. **--genotype_prefix:** Target Genotype Data 
5. **--phenotype_file:** Target Phenotype File 


##prs-port 

**prs-port** estimates a target population PRS without GWAS summary
statistics from the target population by optimising base
population PRS using individual level data from the target
population. **prs-port** is run with the command `./bridgePRS
prs-port run` with the following arguments on the command line or
configuration file:
