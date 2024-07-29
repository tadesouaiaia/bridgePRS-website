![Screenshot](img/slim/guide_logo7.png) 
# Input Data

## LD Reference Data: Custom Data 

BridgePRS requires genotype data in PLINK binary format from samples
representative of the base and target population GWASs.

To pass user supplied LD reference data for a population named
**POP**, create folder a (named **POP_ld**) which includes:

- A **.bed**, **.bim**, and **.fam** file for each chromosome with
  format "chr"[1-22]".ext"
- **POP_ids.txt**, a txt file that lists the sample IDs for your
  population(s)

Then use the command line argument `--ld_path` to point to the
location of this folder on your computer.






