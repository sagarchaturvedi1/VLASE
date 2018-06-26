# VLASE: Vehicle Localization by Aggregating Semantic Edges   

VLASE is a framework to use semantic edge features from images to achieve on-road localization. Semantic edge features denote edge contours that separate pairs of distinct objects such as building-sky, roadsidewalk, and building-ground. While prior work has shown promising results by utilizing the boundary between prominent
classes such as sky and building using skylines, we generalize this approach to consider semantic edge features that arise from 19 different classes. Our localization algorithm is simple, yet very powerful. We extract semantic edge features using a recently introduced CASENet architecture and utilize VLAD framework to perform image retrieval. Our experiments show that we achieve improvement over some of the state-of-the-art localization algorithms such as SIFT-VLAD and its deep variant NetVLAD. We use ablation study to study the importance of different semantic classes, and show that our unified approach achieves better performance compared to individual prominent features such as skylines.
  
## Pre-requisites:  
1. [Casenet](http://www.merl.com/research/license#CASENet)  
2. opencv-2.4.13  
3. Python libraries as listed in the [requirements.txt](https://github.com/sagachat/VLASE/blob/master/requirements.txt)  
  
## Installation:  
1. Install Python 2.7 and the libraries listed in the [requirements.txt](https://github.com/sagachat/VLASE/blob/master/requirements.txt)
2. Install CASENet as per the instructions in it's README file. CASENet includes it's own Caffe version.
3. Extract all the frames from your source video into a directory (We'll call it src). VLASE uses original frames for SIFT features.
4. 
  
## Casenet Usage: 
 

### Casenet Class Ids: 

Casenet is pre-trained on [cityscapes](https://www.cityscapes-dataset.com/) and following classes (with associated class ids) were used:   
  
#### Static :  
0 -> 'road'  
1 -> 'sidewalk'  
2 -> 'building'  
3 -> 'wall'  
4 -> 'fence'  
5 -> 'pole'  
6 -> 'traffic light'  
7 -> 'traffic sign'  
8 -> 'vegetation'  
9 -> 'terrain'  
10 -> 'sky'  
  
#### Dynamic:  
11 -> 'person'  
12 -> 'rider'  
13 -> 'car'  
14 -> 'truck'  
15 -> 'bus'  
16 -> 'train'  
17 -> 'motorcycle'  
18 -> 'bicycle'  
  
  
## Data Preparation:  
  
  
  
  
  
  
  
  
  

  
## Types of experiments:  

### Sift
- Standard  
- Sift with changing the value of alpha (Assign different weights to sift features and xy coordinate features)  
- Sift with changing the number of clusters  
  
### Casenet
- Standard  
- Casenet with changing the value of alpha (Assign different weights to casenet features and xy coordinate features)  
- Casenet with changing the number of clusters  
- Casenet with removing a subset of features (All Static, Combination of some static)  
  
  
## Execution Instructions:  
  
### Build Vocab:  
  
#### Using Casenet   
  
##### Standard
python build_vlad_vocabulary.py -i /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09 -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/AM09/resized -f casenet -c 64 -s 5  
  
##### Remove features -   
python build_vlad_vocabulary.py -i /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09 -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/AM09/resized -f casenet -c 64 -s 5  -crf 11,12,13  
  
##### Change weights of casenet features and XY using alpha
python build_vlad_vocabulary.py -i /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09 -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/AM09/resized -f casenet -c 64 -s 5  -a 0.1  
  
#### Using Sift   
  
##### Standard  
python build_vlad_vocabulary.py -i /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/AM09/resized -s 5  
  
##### Change weights of SIFT features and XY using alpha
python build_vlad_vocabulary.py -i /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/AM09/resized -s 5  -a 0.1  
  
  
### Create VLAD descriptors:  
  
  
#### Using Casenet   
  
##### Standard
python compute_vlad_descriptor.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/all -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/all -f casenet -c 64 -s 5  
  
##### Remove features -   
python compute_vlad_descriptor.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/all -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/all -f casenet -c 64 -s 5 -crf 11,12,13  
  
##### Change weights of casenet features and XY using alpha
python compute_vlad_descriptor.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -r /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/all -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/all -f casenet -c 64 -s 5  -a 0.1  
  
  
  
#### Using Sift   
  
##### Standard  
python compute_vlad_descriptor.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/all -s 5  
  
##### Change weights of SIFT features and XY using alpha
python compute_vlad_descriptor.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -src /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST/all -s 5  -a 0.1  
  

### Localize:  
  
#### Global gps lat & long
python vlad_place_recognition.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -v vocabulary_f=casenet_k=64_t=0.5_alpha=0.5.vlad.npz -g global

#### gps in meters
python vlad_place_recognition.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -v vocabulary_f=casenet_k=64_t=0.5_alpha=0.5.vlad.npz

#### For a specific distance threshold
python vlad_place_recognition.py -tr /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM09_GPS.txt -te /uusoc/exports/scratch/xiny/cvpr18-localization_dataset/KAIST/KAIST_CASENET/AM05_GPS.txt -v vocabulary_f=casenet_k=64_t=0.5_alpha=0.5.vlad.npz -g global -d 10
  
  
## Demo Video:  
  
https://youtu.be/IKZXZmmdtiA
  
  
  
  
  
  
  
  