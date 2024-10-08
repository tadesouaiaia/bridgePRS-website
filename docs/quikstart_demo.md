![Screenshot](img/slim/quikstart_logo2.png)

## Input Data 

This demo runs using the following population config files
**data/pop_AFR/afr.config** and **data/pop_EUR/eur.config** that
list the paths for all required population data. 

## Run The Demo: 

To run BridgePRS using a continuous phenotype: 

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

## Demo Results:


If BridgePRS runs successfully on the toy data, please go to the next
page for information on interpretation of the results.  Before running
BridgePRS with larger real data, please consider reading our [most
common use case examples](guide_usecases.md) to understand how best
to use BridgePRS in realistic scenarios.

    
![Screenshot](img/combo1.png)



