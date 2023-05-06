# Skeleton-MixFormer
This repo is the official implementation for Skeleton-MixFormer: Multivariate Topology Representation for Skeleton-based Action Recognition

# Architecture of SK-MixF







# Prerequisites

+ Python >= 3.6

+ PyTorch >= 1.1.0

+ PyYAML, tqdm, tensorboardX

# Data Preparation

### Download datasets.

**There are 4 datasets to download:**
+ NTU RGB+D 60 Skeleton
+ NTU RGB+D 120 Skeleton
+ NW-UCLA
+ U-Human

**NTU RGB+D 60 and 120**

1. Request dataset: \https://rose1.ntu.edu.sg/dataset/actionRecognition\
2. Download the skeleton-only datasets:
    i. ~~~nturgbd_skeletons_s001_to_s017.zip~~~ (NTU RGB+D 60)
    ii.~~~nturgbd_skeletons_s018_to_s032.zip~~~ (NTU RGB+D 120)
    iii.Extract above files to ~~~./data/nturgbd_raw~~~

**NW-UCLA**

1. Download dataset from [here](https://drive.google.com/file/d/1wWhgqMEQlrCKcJHu6W72Zk_iloS7_JJw/view?usp=share_link)

**U-Human**

1. Download dataset from [here](https://sutdcv.github.io/uav-human-web/)

### UAV-Human-Skeleton-Preprocessing
The processing of the uva dataset is improved from the preprocessing method of the NTU RGB+D dataset in the CTR-GCN source code.  

UAV 3D Human Dataset address: **https://github.com/SUTDCV/UAV-Human**  
CTR-GCN Source code address: **https://github.com/Uason-Chen/CTR-GCN**  
UAV Cross-Subject-v1 Data preprocessed: **https://drive.google.com/file/d/1PzxJohTxu3MbPD9Y1TcxKLJXtfDFNgKp/view?usp=share_link**  
UAV Cross-Subject-v2 Data preprocessed: **https://drive.google.com/file/d/1MwN4iNChfAza8cgJ_T2JCRm2P6rDm6ni/view?usp=share_link**

### Changes to statistics  
### Annotations  

* FileName: **P**000S00G10B10H10UC022000LC021000**A**000**R**0_08241716.txt  

- **P**000: (**P**ersonID) unique person ID for the main subject in current video

+ **A**000: (**A**ction) action labels of current sample  

+ **R**0: (**R**eplicate) replicate capturing  

According to the organization form of UAV-human data set file name, change the person ID(**P**), action repetition (**R**), action classification (**A**) and camera ID(**C**) in static data. Due to different collection methods of data sets, the default uav data is collected by a single camera, so the camera ids corresponding to all samples are set to 0.

### Changes to code 

+ **get_raw_skes_data.py:** Change the **ske_path** of the raw dataset, file extension, file name truncion method, and the size of the generated array used to store the coordinate information of the skeleton node in the current frame.

+ **get_raw_denoisded_data.py:** set **noise_len_thres** = 0, Changing action label truncion way and all the numbers in the code from 25 to 17, 75 to 51, and 150 to 102. 

+ **seq_transformation.py:** Classify the training and testing according to the **https://github.com/SUTDCV/UAV-Human** (here is the reference he gave the first scheme).
~~~
train_ids = [0, 2, 5, 6, 7, 8, 10, 11, 12, 13, 14, 15, 
             16, 17, 18, 19, 20, 21, 25, 26, 27, 28, 29, 
             30, 32, 33, 34, 35, 36, 37, 38, 39, 40, 42, 43, 
             44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 55, 56, 57, 
             59, 61, 62, 63, 64, 65, 67, 68, 69, 70, 71, 73, 76, 77,
             78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 98, 100, 
             102, 103, 105, 106, 110, 111, 112, 114, 115, 116, 117, 118]
test_ids = [1, 3, 4, 9, 22, 23, 24, 31, 41, 58, 60, 66, 72, 74, 75, 91, 92, 
            93, 94, 95, 96, 97, 99, 101, 104, 107, 108, 109, 113]
~~~
### Conclude
After making these changes, running **get_raw_skes_data.py**, **get_raw_denoisded_data.py**, and **seq_transformation.py**, In addition, the data is being cleaned up and stay tuned.**
