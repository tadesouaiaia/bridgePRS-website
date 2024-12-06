![Screenshot](img/slim/req_logo2.png)

# Requirements 

BridgePRS uses [`R`](https://www.r-project.org/) ($\geq$ 3.6.3), `plink`, and runs using a `python3` wrapper. 


## R packages

BridgePRS requires the following `R` packages:   
**BEDMatrix, boot, data.table, doMC, glmnet, MASS, optparse, parallel, and R.utils**

!!! tips "R Packages"
    These packages can be installed from inside an R terminal using the command: 
        ```
        $ R 
        install.packages(c("BEDMatrix","boot","data.table","doMC","glmnet","MASS","optparse","parallel","R.utils")) 
        ```


## Plink 
Plink documentation and downlaod can be found [here](https://www.cog-genomics.org/plink/).

The BridgePRS downlaod includes plink for Linux and MacOs and
the software will attempt to locate the correct version.  To override
this behaviour and use a specific version please use the flag
`--plinkPath` $PLINKPATH to direct BridgePRS
to the file location.  

!!! warning "Extra MacOs Security:"   
    MacOs often block executables if they are not approved from the app store.
    You may have to change your settings to allow Plink to be called  
    For instructions on how to do so, please click [here](req_mac.md).   




## Python
Python3+ can be downloaded 
[here](https://www.python.org/downloads/). Optional plots are created using
the python library [`matplotlib`]
(https://matplotlib.org/stable/users/installing/index.html)).

## Bash
BridgePRS can also be run using a shell script as described
[here](https://github.com/clivehoggart/BridgePRS). Shell scripts that
run the example data are provided with the download.


## BridgePRS check 
Once BridgePRS has been downloaded and made executable the
following command will check system compatibility and prompt you
to install missing software:

```
./bridgePRS check requirements
Checking Requirements:
System:  platform=linux,  cores(available)=8,          cores(used)=1       (TIP: Using More Than One Core Will Improve Performace (e.g. ---cores 7))
Plink:  found=true,      path=/home/tade/Bin/plink
R:  found=true,      path=/usr/bin/R,             version=3.6.3       (packages=up to date)                                            
Python3:  found=true,      path=/usr/bin/python3,     matplotlib=true
    Complete
```

















