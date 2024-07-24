



[//]: # (![Screenshot](img/bridge_logo1.png) 
[//]: # (![Screenshot](img/bridge_logo2.png)
 

![Screenshot](img/fat_logo.png) 


[//]: # (![Screenshot](img/bridge_logo3.png) 


BridgePRS is a **Bayesian** method that utilises **ridge** regression
developed to tackle the "**PRS** Portability Problem".  The PRS
portability problem causes lower PRS accuracy in target populations
not included in the GWAS base used to estimate the PRS. This is due to
differences in linkage disequilibrium (LD), allele frequency and
gene–environment interactions affecting causal effect sizes between
the base and target populations.


<!--
| Operating System | Link | Notes | 
| -----------------|:----------:|:----:| 
| Linux  64-bit | [v1.0.2](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) | Updated 7-12-2024 |  
| Mac  64-bit   | [v1.0.2](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) | Updated 6-27-2024 | 
| Windows       | NA     | Not Available | 

# Reference Panels 
| Source | Link | Notes | 
| -----------------|:----------:|:----:| 
| HapMap | [v1.0.2](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) | Updated 7-12-2024 |  
| 1000G_   | [v1.0.2](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) | Updated 6-27-2024 | 
| Windows       | NA     | Not Available | 
| 1000G Ref Panel | [1000G_ref.tar.gz](https://drive.google.com/file/d/1djAEwRiQsh4veinSLHO3laGjNF95vvN9/view?usp=drive_link) | Optional (Unzip into data directory to use) |    
| 1000G Ref Panel | [1000G_ref.tar.gz](https://drive.google.com/file/d/1djAEwRiQsh4veinSLHO3laGjNF95vvN9/view?usp=drive_link) | Optional (Unzip into data directory to use) |    
-->







# Download Links 


|BridgePRS Packages |Reference Panels|
|--|--|
|<table> <tr><th> OS </th><th> Link </th><th> Last Update  </th></tr>  <tr><td> Linux 64-Bit </td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) </td><td> 7-12-2024 </td></tr>  </th></tr>  <tr><td> Mac 64-Bit </td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) </td><td> 6-16-2024 </td></tr> </th></tr>  <tr><td> Windows </td><td> NA </td><td> Not Available </td></tr> </table> | <table> <tr><th> Download Link  </th><th> Size </th><th> More Information </th></tr><tr><td> [HapMap variants](https://drive.google.com/file/d/1NElCu-QYS4qniZ6og5ar7eXjiQVWPTmh/view?usp=drive_link) </td><td> <1GB </td><td> [International HapMap Project](https://www.genome.gov/10001688/international-hapmap-project) </td></tr>  </th></tr>  <tr><td> [1000 Genomes variants: MAF>5%](https://drive.google.com/file/d/1nzsXnQa3Zdl0PpJGOADs8EqAPSOdYnKY/view?usp=drive_link) </td><td> 8GB </td><td> [International Genome Sample Resource](https://www.internationalgenome.org/) </td></tr> </th></tr>  </td><td> [1000 Genomes variants: MAF>1%](https://drive.google.com/file/d/16IpkBXnuy9xgwxFPglJTDzyGjmUqha6q/view?usp=drive_link) </td><td> 14GB </td><td> [International Genome Sample Resource](https://www.internationalgenome.org/) </td></tr> </table>



<!--
|BridgePRS Package |Reference Panels|
|--|--|
|<table> <tr><th> OS </th><th> Link </th><th> Last Update  </th></tr>  <tr><td> Linux 64-Bit 
</td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) 
</td><td> 7-12-2024 </td></tr>  </th></tr>  <tr><td> Mac 64-Bit 
</td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) 
</td><td> 6-16-2024 
</td></tr> </th></tr>  <tr><td> Windows </td><td> NA </td><td> Not Available </td></tr> </table>       
| <table> <tr><th>Source</th><th>Link  </th><th> Notes </th></tr><tr><td> HapMap </td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) 
</td><td> Cool </td></tr>  </th></tr>  <tr><td> 1k Genomes </td><td> [v1.0.3](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) 
</td><td> Cool </td></tr> </th></tr>  <tr><td> Windows </td><td> [v1.0.03](www.google.com) 
</td><td> Cool </td></tr> </table>     
-->




!!! Note "Latest Updates"
    # 2023-09-15 (v0.1.7)
    - We have added sample thousand genomes data. 
    - update log can be found [here](misc_log.md)

# Overview 

- BridgePRS is written in R with a Python
  wrapper. [Plink.](https://www.cog-genomics.org/software) is used in
  the first stage of the modelling for clumping and thresholding (all
  markers within clumps are retained for analysis).
  For more information on installing dependencies, please refer to [Requirements](req_software.md). 
- To get BridgePRS running using toy data see our [Quick Start Tutorial.](quikstart_data.md).
- Following the Quick Start, the full guide provides more [realistic examples](guide_usecases.md) to help you get started with your own data. 




!!! Warning "Citation: Our Manuscript is published in Nature Genetics" 
    Please cite our [paper](https://www.nature.com/articles/s41588-023-01583-9): 
 
    Hoggart C, Choi SW, García-González J, Souaiaia T, Preuss M, O'Reilly P. BridgePRS leverages shared genetic effects across ancestries to increase polygenic risk score portability. Nat Genet 56, 180–186 (2024).
    https://doi.org/10.1038/s41588-023-01583-9





## Contact 
For questions about the methodology, this website, or our manuscript
please contact [Dr Clive Hoggart](http://www.pauloreilly.info/), [Dr
Tade Souaiaia](http://www.pauloreilly.info/), or [Dr Paul
O'Reilly](http://www.pauloreilly.info/).  For source code and coding
issues please visit the bridgePRS github
[here](https://github.com/clivehoggart/BridgePRS).


## Acknowledgements

We would like to thank Brian Fulton-Howard for his feedback and help with testing. 







