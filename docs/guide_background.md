![Screenshot](img/slim/guide_logo1.png)



BridgePRS is a trans-ancestry PRS software which improves polygenic
risk score analysis in under-represented target populations by
combining summary statistics from under-represented target populations
(e.g. Africans) with those from a powerful GWAS (e.g. Europeans).


# Background

PRS methods require as input summary statistics from genome wide association
studies. If unfamiliar with GWAS or in need of a refresher consider reading
[this paper](https://www.ncbi.nlm.nih.gov/pubmed/29484742).

- Genome-wide association studies (GWAS) involve analyzing the genomes
  of a large group of individuals.  
- For a binary trait (like blue or brown eyes) this involves comparing
the frequency of genetic variations in each group to produce an
odds-ratio (measure of association) and a p-value to measure the
signficance of the realtionship at each SNP.
- For continuous measures (like height) this results in an effect size (measure of continuous association) 
  and p-value that measure the significance of our relationship.   
- GWAS results can be summarized in a sumstats file which looks like this:


CHR|ID|REF|A1|A1_FREQ|OBS_CT|SE|BETA|P|                                                                                                                                 
:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|                                                                                                                                                                                                  
1|rs100|A|T|0.1|100|0.01|1.10|0.01                                                                                                  
2|rs200|C|G|0.2|100|0.02|-1.10|0.05                                                                                                  
3|rs300|G|A|0.3|100|0.03|1.02|0.10                                                                                                  



# PRS basics

- Polygenic scores combine genetic variant associations genome-wide by 
  summing their effects to produce individual scores that predict the phenotype.   
- Different PRS methods use different statistical methods to select
  variants and estimate their effect sizes for use in the PRS.
- BridgePRS, like many other PRS methods, requires genotype and
  phenotype data from individuals (several hundred samples) in
  addition to GWAS summary statistics to estimate the PRS. 
- The predictive power of PRS is assessed in genotype and phenotype
  data from unseen samples. BridgePRS reports PRS accuracy by the
  residual variance explained $R^2$ (accounting for the variance
  explained by the non-genetic covariates included in the model). For
  binary traits Nagelkerke $R^2$ is used.


# Cross Population Analysis 

**The PRS Portability Problem**

- Often when a PRS trained using data from one population,
  e.g. European, is applied to a population of a different ancestry,
  e.g. African, the PRS model is less predictive.
- Often there is insufficient data in the non-European population to
  estimate good ancestry specific PRS using this data alone. Using
  single ancestry PRS methods researchers are left with two choices:
    - An underpowered PRS model estimated using only data the target
      (non-European) population.
    - A PRS estimated using a well powered GWAS from Europeans



**The BridgePRS Solution**

- BridgePRS combines GWAS summary statistics from two populations,
  typically a large well powered GWAS from a "base" population
  (e.g. European) and a smaller GWAS from the target population
  (e.g. African).
- Figure 1 of our [Nature Genetics
  Paper](https://www.nature.com/articles/s41588-023-01583-9) gives an
  overview of the modelling implemented by BridgePRS.
- Figure 1 shows the three models, M1-3, estimated by BridgePRS which
  are subsequently  combined to give the final PRS. Below we outline
  these three models
- Model M1: BridgePRS uses two prior distributions to estimate PRS which we
  describe as Stage 1 and Stage 2. Stage 1 analysis is a single
  population analysis and applies zero centred Gaussian prior
  distributions to SNP effect sizes within clumps. Stage 2 uses the
  output from a Stage 1 analysis of the base population as the prior
  for the target population.
- Model M2: This is a single population analysis using Stage 1 analyis
  applied to the target populationto produce two
  sets of SNP weights
- Model M3: M1 and M2 both produce PRS estimated under different prior
  parameter settings. These PRS are combined in a ridge regression fit
  to the target data to give models M1 and M2. Model M3 is estimated
  by combining both sets of PRS in a ridge regression fit.
- Model M1 reflects the belief that the target population GWAS is only
  informative in conjugtion with the base population GWAS.
- Model M2 reflects the belief that the target population GWAS is
  informative and the base population GWAS gives no addition
  information.
- Models M3 reflects the belief both the base and
  target population GWAS contribute independent information.
-  Since we do not know apriori which of the three scenarios (M1, M2,
   or M3) are true, BridgePRS weights and sums all three models to
   produce and evaluate a single target population PRS.  BridgePRS
   also reports SNP weights and PRS R2 values in the target population
   for each of the three other models (M1, M2, or M3), enabling the
   user to use any of the four models.
- Further detals outlining this modelling is shown in Figure 1 of our
  [Nature Genetics Paper](https://www.nature.com/articles/s41588-023-01583-9)









