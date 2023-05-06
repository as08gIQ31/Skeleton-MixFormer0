# Skeleton-MixFormer
This repo is the official implementation for Skeleton-MixFormer: Multivariate Topology Representation for Skeleton-based Action Recognition

# Architecture of SK-MixF







# Prerequisites

+ Python >= 3.6

+ PyTorch >= 1.1.0

+ PyYAML, tqdm, tensorboardX

# Data Preparation

### Download datasets

**There are 4 datasets to download:**
+ NTU RGB+D 60 Skeleton
+ NTU RGB+D 120 Skeleton
+ NW-UCLA
+ U-Human

**NTU RGB+D 60 and 120**

1. Request dataset: https://rose1.ntu.edu.sg/dataset/actionRecognition
2. Download the skeleton-only datasets:  
    i. ```nturgbd_skeletons_s001_to_s017.zip``` (NTU RGB+D 60)  
    ii. ```nturgbd_skeletons_s018_to_s032.zip``` (NTU RGB+D 120)  
    iii. Extract above files to ```./data/nturgbd_raw```  

**U-Human**

1. Download dataset from here: https://sutdcv.github.io/uav-human-web/
2. Move ```Skeleton``` to ```./data/UAV-Human```

**NW-UCLA**

1. Download dataset from [here](https://drive.google.com/file/d/1wWhgqMEQlrCKcJHu6W72Zk_iloS7_JJw/view?usp=share_link)
2. Move ```all_sqe``` to ```./data/NW-UCLA```



### NTU Data Processing

#### Directory Structure

Put downloaded data into the following directory structure:
~~~
- data/
  - UAV-Human/
    - Skeleton
      ... # raw data of UAV-Human
  - NW-UCLA/
    - all_sqe
      ... # raw data of NW-UCLA
  - ntu/
  - ntu120/
  - nturgbd_raw/
    - nturgb+d_skeletons/     # from `nturgbd_skeletons_s001_to_s017.zip`
      ...
    - nturgb+d_skeletons120/  # from `nturgbd_skeletons_s018_to_s032.zip`
      ...
~~~

#### Generating Data

+ Generate NTU RGB+D 60 or NTU RGB+D 120 dataset:
~~~
 cd ./data/ntu # or cd ./data/ntu120
 # Get skeleton of each performer
 python get_raw_skes_data.py
 # Remove the bad skeleton 
 python get_raw_denoised_data.py
 # Transform the skeleton to the center of the first frame
 python seq_transformation.py
~~~

### UAV Data Processing

+ Generate UAV-Human dataset:

+ Changes to statistics  
**Annotations**  

1. FileName: **P**000S00G10B10H10UC022000LC021000**A**000**R**0_08241716.txt  

2. **P**000: (**P**ersonID) unique person ID for the main subject in current video

3. **A**000: (**A**ction) action labels of current sample  

4. **R**0: (**R**eplicate) replicate capturing  

According to the organization form of UAV-human data set file name, change the person ID(**P**), the number of action repetition (**R**), action classification (**A**) and camera ID(**C**) in static data. Due to different collection methods of data sets, the default uav data is collected by a single camera, so the camera ids corresponding to all samples are set to 0.

+ Changes to code 

1. ```get_raw_skes_data.py``` Change the **ske_path** of the raw dataset, file extension, file name truncion method, and the size of the generated array used to store the coordinate information of the skeleton node in the current frame.

2. ```get_raw_denoisded_data.py``` set **noise_len_thres** = 0, Changing action label truncion way and all the numbers in the code from 25 to 17, 75 to 51, and 150 to 102. 

3. ```seq_transformation.py``` Classify the training and testing according to the https://github.com/SUTDCV/UAV-Human. 

Request detailed pre-processing steps or preprocessed dataset [here](https://github.com/back330/UVA-Human-Skeleton-Preprocessing)  
# Contact
For any questions, feel free to contact: ly330@stu.xidian.edu.cn
