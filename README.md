# Tensorflow Code for the paper: 
*[S-VVAD: Visual Voice Activity Detection by Motion Segmentation](Link)

## Overview
![BlockDiagram](https://github.com/muhammadshahidwandar/S-VVAD/blob/master/diagrams/Fig_Main.jpg)

The Method consist of following steps as shown in figure above

1. Training a ResNet50 model with the pre-trained weights used for network initialization. We used code from (RealVAD)(https://github.com/muhammadshahidwandar/Visual-VAD-Unsupervised-Domain-Adaptation) for this step  

2. Class activation map generation using Gradient-CAM for Voice Activity Detection (VAD) labels: 0: not-speaking, 1: speaking. We used code from (RealVAD)(https://github.com/muhammadshahidwandar/Visual-VAD-Unsupervised-Domain-Adaptation)

3. VAD-motion-cues-based mask generation.
 
4. Fully Convolution Network (FCN) training using VAD-cues' generated Masks in step 3.

## Sub-directories and Files
There are three sub-directories described as follows:

### Images
Containes some sample dynamic images with their coresponding mask generated images used for the training of FCN

### Modified-Columbia
Containes some sample train and validation set for modified-columbia dataset as explained in S-VVAD paper.  

### Resnet-Finetuning

``Train_Main``: To train ResNet model on a given dataset 

``Test_Main.py``: Test the trained model on a single image

``Model_Evaluation.py``: To evaluate the trained model on a complete test set

``FcMatWritter.py``: To write extracted fc features into a .mat file

``Resnet.py``: ResNet model definition

``datageneratorBalancedBatch.py``: Image batch generator with balanced number of samples from each class

``datageneratorSequenceBatch.py``: Sequential image batch generator

### Unsupervised-DomainAdaptation-Matlab

``VAD_Domain_Adaptation.m``: Training and test unsupervised domain adaptation when the ResNet fc features are the input

Some pre-trained ResNet50 model can be downloaded from this link (https://drive.google.com/drive/folders/1dHYOMuzXHL46P1zDgDyDj9NgYzV1nNSS?usp=sharing)

## Dependencies
* Python 3.5
* Tensorflow 1.12
* Opencv 3.0
* Natsort 7.0.1
* Matlab 2017b

## How it works
1- Obtain your target datasets e.g.  RealVAD (https://github.com/IIT-PAVIS/Voice-Activity-Detection)

2- Generate and save the dynamic image by using (https://github.com/hbilen/dynamic-image-nets) 

3- Define your training and test folds in the text files (example files as given as trainRealVAD1.txt and testRealVAD1.txt in RealVAD sub-directory)

4- Change paths and parameters in Train_Main.py to train ResNet model

5- Evaluate trained model on test set by using Model_Evaluation.py

6- Any single dynamic image can be tested by using Test_Main.py 

7- Save fc feature for training and test data in .mat file using FcMatWritter.py

8- Run VAD_Domain_Adaptation.m in matlab to perform and test Unsupervised Domain Adaptation component

## Reference

**RealVAD: A Real-world Dataset for Voice Activity Detection**  
Cigdem Beyan, Muhammad Shahid and Vittorio Murino,
```
@ARTICLE{Beyan2020TMM,
  author={C. {Beyan} and M. {Shahid} and V. {Murino}},
  journal={IEEE Transactions on Multimedia},
  title={RealVAD: A Real-world Dataset and A Method for Voice Activity Detection by Body Motion Analysis},
  year={2020},
  volume={},
  number={},
  pages={1-1},}
```
**Voice Activity Detection by Upper Body Motion Analysis and Unsupervised Domain Adaptation**  
Muhammad Shahid, Cigdem Beyan and Vittorio Murino, ICCVW 2019
```
@inproceedings{shahid2019voice,
  title={Voice Activity Detection by Upper Body Motion Analysis and Unsupervised Domain Adaptation},
  author={Shahid, Muhammad and Beyan, Cigdem and Murino, Vittorio},
  booktitle={Proceedings of the IEEE International Conference on Computer Vision Workshops},
  pages={0--0},
  year={2019}
}
```
