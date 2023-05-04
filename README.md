# Skeleton-MixFormer
## UVA-Human-Skeleton-Preprocessing
The processing of the uva dataset is improved from the preprocessing method of the NTU RGB+D dataset in the CTR-GCN source code.  

UVA 3D Human Dataset address: https://github.com/SUTDCV/UAV-Human  
CTR-GCN Source code address: https://github.com/Uason-Chen/CTR-GCN  
UVA Cross-Subject-v1 Data preprocessed: https://drive.google.com/file/d/1PzxJohTxu3MbPD9Y1TcxKLJXtfDFNgKp/view?usp=share_link  
UVA Cross-Subject-v2 Data preprocessed: https://drive.google.com/file/d/1MwN4iNChfAza8cgJ_T2JCRm2P6rDm6ni/view?usp=share_link

+ Changes to statistics  
According to the organization form of UAV-human data set file name, change the person ID(P), the number of passes performed by the action (R), the classification of the action (A), and the camera ID(C) in the static data. Due to different collection methods of data sets, the default uav data is collected by cameras, so the camera ids corresponding to all samples are set to 0.
