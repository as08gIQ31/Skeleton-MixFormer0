# Skeleton-MixFormer
## UVA-Human-Skeleton-Preprocessing
The processing of the uva dataset is improved from the preprocessing method of the NTU RGB+D dataset in the CTR-GCN source code.  

UVA 3D Human Dataset address: https://github.com/SUTDCV/UAV-Human  
CTR-GCN Source code address: https://github.com/Uason-Chen/CTR-GCN  
UVA Cross-Subject-v1 Data preprocessed: https://drive.google.com/file/d/1PzxJohTxu3MbPD9Y1TcxKLJXtfDFNgKp/view?usp=share_link  
UVA Cross-Subject-v2 Data preprocessed: https://drive.google.com/file/d/1MwN4iNChfAza8cgJ_T2JCRm2P6rDm6ni/view?usp=share_link

### Changes to statistics  
#### Annotations  

* FileName: **P**000S00G10B10H10UC022000LC021000**A**000**R**0_08241716.txt  

- **P**000: (PersonID) unique person ID for the main subject in current video

+ **A**000: (Action) action labels of current sample  

+ **R**0: (Replicate) replicate capturing  

According to the organization form of UAV-human data set file name, change the person ID(**P**), action repetition (**R**), action classification (**A**) and camera ID(**C**) in static data. Due to different collection methods of data sets, the default uav data is collected by a single camera, so the camera ids corresponding to all samples are set to 0.

Change the **ske_path** of the raw dataset, file extension, file name interception method, and the size of the generated array used to store the coordinate information of the skeleton node in the current frame

set **noise_len_thres** = 0, Changing action label truncion way and all the numbers in the code from 25 to 17, 75 to 51, and 150 to 102. 

Classify the training and testing according to the **https://github.com/SUTDCV/UAV-Human** amend the 197-205 lines of code is as follows (here is the reference he gave the first scheme).
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
