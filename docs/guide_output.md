![Screenshot](img/slim/guide_logo5.png) 
# Output Data


For every PRS invocation of BridgePRS (single, port, and prior) BridgePRS produces the following 
output files.  Weighted combined versions of each files of also produced by BridgePRS in the folder 
`prs-combined_POP1-POP2`.  These files are: 


|Name|file extension|Contents|
|:-:|:-:|:-:|
|SNP Weights|.snp_weights.dat|SNP weights for this model stage of BridgePRS| 
|Performance Result|.var_explained.txt|$R^2$ in validation samples for the models at this stage of BridgePRS| 
|PRS Values|.preds.dat|Predicted Continuous Phenotype Values or Risk Scores (PRS)| 
|Progress Plot|bridgePRS-{subProgram}.png|Performance Summary| 









