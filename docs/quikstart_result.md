![Screenshot](img/slim/quikstart_logo3.png)

# Interpreting results 

The easyrun command used in the previous step runs the following
[subprograms](guide_pipeline.md):

1. `prs-single (stage 1):` [Applied to the base population
   (Eur). Used to define prior for target population PRS.](guide_pipeline.md#build-single)
2. `prs-prior (stage 2):` [Applied to the target population (AFR)
   PRS using prior estimated from base population (Eur).](guide_pipeline.md#prs-prior)  
3. `prs-single (stage 1): ` [Applied to the target population (Afr).
   PRS estimated using target population data only.](guide_pipeline.md#prs-single) 
4. `analyse` [Combine Afr stage 1 and 2 results to produce a weighted
   target PRS result.](guide_pipeline.md#prs-prior)
5. `prs-port:   `     [Base population PRS applied to target population.](guide_pipeline.md#prs-port) 

And produces output in the following five subdirectories: 

1. **prs-single_AFR/quantify/:** Weights, predictions, and performance metrics. 
2. **model_EUR/prior:**          Model weights and priors. 
3. **prs-prior_AFR/quantify/:**  Weights, predictions, and performance metrics. 
4. **prs-combined_AFR/:**        Analysis that combined the previous three steps. 

3. **prs-port_AFR/quantify/:**   Weights, predictions, and performance metrics. 
