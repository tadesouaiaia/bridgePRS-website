![Screenshot](img/slim/quikstart_logo3.png)

# Interpreting results 

The pipeline command used on the previous page runs the entire bridgePRS multi-ancestry 
analysis. Final model results are written to the directory
`prs-combined_AFR-EUR/`, the important files are:

File|Contents|
:------------------------|:------------------------|
 `AFR_weighted_combined_var_explained.txt` | $R^2$ of the four models estimated by BridgePRS  and contribution (weights) of models M1-3 to the final weighted model see [pipeline](guide_background.md)|
 `AFR_weighted_combined_preds.dat` | Individual PRS of the four model in validation samples |
 `AFR_weighted_combined_snp_weights.dat` | SNP weights for the weighted model |



