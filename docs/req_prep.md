![Screenshot](img/slim/req_logo1.png)

## Preparation 


After [downloading](https://github.com/clivehoggart/BridgePRS/archive/refs/heads/main.zip) and unzipping BridgePRS 
into a suitable directory on your machine you will observe that a folder with the following contents: 
    
     bridgePRS              <--- program executable 
     data/                  <--- input data               
     LICENSE
     README.me 
     src/                   <--- source code 
     tests/                 <--- test directory 

!!! tip "Using the terminal, type the following command from within the directory:" 
    ``` 
    chmod +x bridgePRS
    chmod +x src/Python/Xtra/plink*
    ``` 
    to make bridgePRS and plink executable 


## Requirements 

Next, confirm that the required libraries and dependencies are installed and available by following 
the instructions in [Software.](req_software.md) 
Alternatively, you can type: 
=== "./bridgePRS check requirements"  
and bridgePRS will check your system and provide further instructions to help you install missing dependencies. 


!!! warning "Warning: Extra MacOs Security:" 
    If you see this msg when running 'check requirements' (or any other time): 
    ![Error](img/mac_plink.png)
    
    You will have to change your system settings to allow bridgePRS to call plink.  
    For instructions on how to do so, please click [here](req_mac.md). 


