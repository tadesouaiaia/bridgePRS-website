![Screenshot](img/slim/guide_logo1.png)



BridgePRS is a trans-ancestry PRS software which improves polygenic
risk score analysis in under-represented target populations by
combining summary statistics from under-represented target populations
(e.g. Africans) with those from a powerful GWAS (e.g. Europeans).


# Background

PRS require as input summary statistics from genome wide association
studies. If you are unfamiliar with GWAS or need a refresher consider reading
[this paper](https://www.ncbi.nlm.nih.gov/pubmed/29484742).

- Genome wide association studies (GWAS) involve analyzing the genomes of a larger group of individuals.  This involves looking screening 
millions of genetic variants (SNP) for association with a particular trait.  
- For a binary trait (like blue or brown eyes) this involves comparing the frequency of genetic variations in each group to produce an odds-ratio (measure of association) and a p-value to measure the 
signficance of the realtionship at each SNP. 
- For continuous measures (like height) this results in an effect size (measure of continuous association) and p-value that measure the significance of our relationship.   

- GWAS results can be summarized in a sumstats file which looks like this: 


|SNP|BP|REF|ALT|BETA|PV|NOTES
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|rs3094315|10523|A|G|1.491|0.0029|Positive ($>1$) Trait Association|
|rs3131972|91345|A|G|0.817|0.0008|Negative ($<1$) Trait Association|
|rs3131971|23040|T|C|1.001|0.5332|Insignificant ($PV>0.05$) Association|

**PRS basics**

- Creating individual polygenic scores involves combine information
  across many genetic variants.  A score is calculated by summing the
  genetic association values (beta-weights) for each allele in an
  individual, therefore, variants with stronger associations have
  a larger impact on the overall score.
- PRS software use different statistical methods to select variants
  and estimate their effect sizes beta for use in the PRS.
- BridgePRS, like many other PRS methods, require genotype and
  phenotype data from  individuals (several hundred samples) in
  addition to GWAS summary statistics to estimate the PRS. 
- The predictive power of PRS is assessed in genotype and phenotype
  data from unseen samples. BridgePRS reports PRS accuracy by the
  residual variance explained $R^2$ (accounting for the variance
  explained by the non-genetic covariates included in the model). For
  binary traits Nagelkerke $R^2$ is used.


## Cross Population Analysis 

**The PRS Portability Problem**

- Often when PRS results from a large test population (usually of European ancestry) are validated to an out of sample population of different ancestry the PRS model is not predictive.  
- Unfortunately, there is not enough data in the non-european population to produce a reliabile "test dataset" so researchers have to either accept either: 
    - An underpowered PRS model made using only the non-european population. 
    - A large PRS model based on European test data that doesn't perform well. 



**The BridgePRS Solution**

- BridgePRS solves this problem by first running producing three different PRS-models. 
    - PRS ran using only the target (Non-European) dataset  
    - PRS ran using SNP-weights calculated from the European Model 
    - PRS ran using a prior effect-size distribution from the European Model  
- Then BridgePRS combines these results to produce a weighted PRS solution. 













