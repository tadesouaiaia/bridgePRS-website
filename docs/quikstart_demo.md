![Screenshot](img/slim/quikstart_logo2.png)

BridgePRS download comes with example toy data in the folders
`data/pop_AFR`, `data/pop_EUR` and `data/pop_EAS`. Each directory
contains (1) GWAS summary stats file(s), (2) genotype file(s) (plink
format), and (3) phenotype file(s) (txt format).  For more information
on file type requirements or how to create population configuration
files for your own data, see [Guide: Input Data](guide_input.md).

BridgePRS uses configuation files to which label the population
analysed, list the paths for the input data and describe the column
header of the summary statistics files. Three example configuations
files are provided, one for each population: `data/eur.config`,
`data/afr.config`, `data/eas.config`. These files


## Run the demo: 

To run BridgePRS with the continuous phenotype in the example data: 

!!! tips "Easyrun Command: Continuous Trait (y)" 
     Run BridgePRS on the toy phenotype "y" with the following command: 
        ```
        ./bridgePRS pipeline go -o out1 --config_files data/afr.config data/eur.config --phenotype y 
        ```


And verify that a summary figure `out1/bridgeSummary.png` shown below is created.  Then repeat the 
process using a binary phenotype: 





!!! tips "Easyrun Command" 
    Run BridgePRS on the toy binary phenotype "y.binary" with the following command: 
        ```
        ./bridgePRS pipeline go -o out2 --config_files data/afr.config data/eur.config --phenotype y.binary
        ```

## Results:


If BridgePRS runs successfully on the toy data, please go to the next
page for information on interpretation of the results.  Before running
BridgePRS with larger real data, please consider reading our [most
common use case examples](guide_usecases.md) to understand how best
to use BridgePRS in realistic scenarios.

    
![Screenshot](img/combo1.png)



