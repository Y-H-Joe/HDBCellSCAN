# HDBCellSCAN
Hierarchical density-based clustering method to detect ROIs in two-photon Ca imaging data
[<img src="https://github.com/hamaguchikosuke/HDBCellSCAN/blob/master/CaGui/figures/HDBCellSCAN_ROIs.png" width=400px>](https://youtu.be/8SzqegNeZCc)
# I. Introduction
HDBCellSCAN is an fast algorithm to detect ROIs based on the idea that within an ROI, pixels must have correlated fluorescent signals. Thus, by assigning virtual distance as 1-correlation between nearest-neighbor pixels, ROI detection problem becomes clustering problem embedded in the noise. To provide a complete pipeline of data analysis, large portion of [Suite2P](https://github.com/cortex-lab/Suite2P), such as image registration and signal extraction codes were used. Spike deconvolution is based on Fast-Oopsi. Thus, this package of HDBCellSCAN provides a complete set of functions to analyze Ca image data; 1) read large Tiff (>4GB) stacks, 2) register images (rigid body), 3) detect ROIs (HDBCellSCAN), 4) GUI to semi-automatically filter ROIs, 5) extract fluorescent signal, and 6) estimate action potential events. Our custamized GUI is equipped with movie player to check raw data, Support-Vector Machine for ROI classification, and ROI split function (see [teaser](https://youtu.be/8SzqegNeZCc)). These pipelined processes can be separately run through HDBCellSCAN_Master.m.

# II. Installation. 
**Requirement**

To run HDBCellSCAN, I recommend 

**MATLAB 2017b** or higher

**Python 3.5 or higher** and hdbscan package 

older versions were not fully tested. 

### Install Python and hdbscan ###

1. Download [Anaconda](https://www.anaconda.com/download/) and install. If you use 64bit OS, install 64bit version. 

2. Open Anaconda. Make a new environment. 
   Put a name like "CaImaging" for that environment.

3. Open terminal by right-clicking the triangle button in "CaImaging" environment.  
   
Type 
\>> conda install -c conda-forge hdbscan

During the installation, you can find the environment location, such as 
C:\Users\hammer\AppData\Local\conda\conda\envs\CaImaging

The hdbscan package is in 
C:\Users\hammer\AppData\Local\conda\conda\envs\CaImaging\Lib\site-packages

Please write down this path and add python path (see How2Use_HDBCellSCAN.m) so that MATLAB can reach to hdbscan packages. 

4. Go to Github [HDBCellSCAN](https://github.com/hamaguchikosuke/HDBCellSCAN) page.

5. Download HDBCellScan package and unzip the downloaded folder.
Hereafter, I assume that HDBCellSCAN is extracted in \<RootDir\>=C:\home\GitHub\HDBCellSCAN

6. To confirm hdbscan package is working in Python, install and launch Spyder from Anaconda. 
Open C:\home\GitHub\HDBCellSCAN\hdbscan_test20171017.py and run each section of the code.
You may face errors of missing package, then please install it from Anaconda.
 
### Run HDBCellSCAN ###
7. Start MATLAB, move to \<RootDir\>. 

8. In the command prompt of MATLAB, type
\>>pyversion

to confirm you have access to python from MATLAB. If it returns empty, you need to install Python or need to set PATH variable (see trouble shooting). 

9. Open an example file, <RootDir>\How2Use_HDBCellScan.m
 You can see how to operate HDBCellScan in this code.

# III. Sample Data
[20 frame averaged data](https://drive.google.com/open?id=1AZ6vBrWiMOHIOn4_DpTgvZkw6IhVUt4u)

# IV. Trouble shooting (in Windows)

### 1. pyversion returns empty 

Recent Anaconda does not recommend to set PATH during the installation. 
You need to set PATH variable by going to 
My Computer -> Properties -> Advanced -> Environment Variables and edit "Path" variable to add Python Path i.e. 'C:\<python_library>'

Another possibility is the version compatibility.
(please check https://jp.mathworks.com/matlabcentral/answers/229501-matlab-do-not-recongnize-pyversion)

### 2. svmtrain returns an error 
Note that I use libsvm (https://www.csie.ntu.edu.tw/~cjlin/libsvm/) to run SVM instead of matlab's toolbox. 
This is in part due to historical reason. In my GitHub commit, svmtrain and svmpredict are already compiled for Windows 64bit, but not for the other environments (since I do not access to Mac/Linux environment).
Please compile them using make.m in libsvm folder.


