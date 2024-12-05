![Screenshot](img/slim/quikstart_logo2.png)

BridgePRS download comes with example toy data in the folders
`data/pop_AFR`, `data/pop_EUR` and `data/pop_EAS`. Each directory
contains (1) GWAS summary stats file(s), (2) genotype file(s) (plink
format), and (3) phenotype file(s) (txt format). A continuous and
binary phenotype are given in the phenotype files, both phenotypes use
the same summary statistics, For more information on file type
requirements or how to create population configuration files for your
own data, see [Guide: Input Data](guide_input.md).

BridgePRS uses configuation files to which label the population
analysed, list the paths for the input data and describe the column
header of the summary statistics files. Three example configuations
files are provided, one for each population: `data/eur.config`,
`data/afr.config`, `data/eas.config`. These files


## Run the demo: 

To analyses the continuous trait (y)
```
./bridgePRS pipeline go -o out1 --config_files data/afr.config data/eur.config --phenotype y 
```


Verify that a summary figure `out1/bridgeSummary.png` shown below is
created.  Then repeat the process using a binary phenotype:


To analyse the binary phenotype "y.binary" 
        ```
        ./bridgePRS pipeline go -o out2 --config_files data/afr.config data/eur.config --phenotype y.binary
        ```

## Results:

If BridgePRS runs successfully on the toy data, go to the next
page for information on interpretation of the output result directories.

    
![Screenshot](img/combo1.png)



