# Tensorflow Code for the paper: 
*[S-VVAD: Visual Voice Activity Detection by Motion Segmentation](Link)-- PAPER LINK will be announced soon, stay tuned!

## Overview
![BlockDiagram](https://github.com/muhammadshahidwandar/S-VVAD/blob/master/images/Fig_Main.jpg)

S-VVAD consists of following steps as shown in the above Figure

1. Training a ResNet50 model with the pre-trained weights used for network initialization. 
Any framework such as tensorflow, pytorch or Caffe can be used. 
We used our previous code that can be found in: (https://github.com/muhammadshahidwandar/Visual-VAD-Unsupervised-Domain-Adaptation) for this step.  

2. Class activation map (CAM) generation using Gradient-CAM for Voice Activity Detection (VAD) labels: 
0: not-speaking, 1: speaking. We used the code taht can be found in: (https://github.com/insikk/Grad-CAM-tensorflow).

3. VAD-motion-cues-based mask generation.
 
4. Fully Convolution Network (FCN) training by using the masks generated in Step 3.

5. Testing Fully Convolution Network (FCN) using test dynamic images and saving the predictions.

6. Bounding box generation using affinity propagation clustring algorithm.
One can use the following code for this step: (https://scikit-learn.org/stable/modules/generated/sklearn.cluster.AffinityPropagation.html)

## Sub-directories and Files
There are four sub-directories described as follows:

### images
Contains the block diagram of S-VVAD training, and some sample images such as CAMs for speaking and not-speaking overlayed on dynamic images and raw CAMs, mask generation images.

### VAD-Mask-Generation
Contains some sample training and test sets for modified-columbia dataset as explained in S-VVAD paper.  

### FCN-Training

``FCN_Train_Main``: To train Fully Convolutional ResNet-50 model on a given dataset 

``resnet_fcn.py``: ResNet-based FCN model definition

``datageneratorModifiedColumbia.py``: Image batch generator: segmentation mask and bounding box for each image

``datageneratorTest.py``: Sequential image batch generator with boundign box annotation

### FCN-Testing

``TestFCN_Main``: To reload and test the trained FCN model on a test set and to save the generated masks

``datageneratorTest.py``: To test image batch geneartor 

Some pre-trained ResNet50 model for tensorflow can be downloaded from this link (https://drive.google.com/drive/folders/1dHYOMuzXHL46P1zDgDyDj9NgYzV1nNSS?usp=sharing)

## Dependencies

* Python 3.5
* Tensorflow 1.12
* Opencv 3.0
* Natsort 7.0.1
* scipy  0.16.0


## How it works
1- Obtain your target datasets, e.g.,  RealVAD Dataset (https://github.com/IIT-PAVIS/Voice-Activity-Detection)

2- Generate and save the multiple dynamic images by using (https://github.com/hbilen/dynamic-image-nets) 

3- Define your training and test folds in the text files (example files given as trainRealVAD1.txt and testRealVAD1.txt under the ValidationFold sub-directory)

4- Change paths and parameters in FCN_Train_Main.py to train ResNet model

5- Test model on a test set by using Model_Evaluation.py and bounding box projection on speaking not-speaking segmentation.


## Reference

**S-VVAD: Visual Voice Activity Detection by Motion Segmentation**  
Muhammad Shahid, Cigdem Beyan and Vittorio Murino, IEEE Winter Conference on Applications of Computer Vision (WACV), 2021.
```
@inproceedings{shahid2020_WACV,
  title={Visual Voice Activity Detection by Motion Segmentation},
  author={Shahid, Muhammad and Beyan, Cigdem and Murino, Vittorio},
  booktitle={2021 IEEE Winter Conference on Applications of Computer Vision (WACV)},
  pages={0--0},
  year={2021}
}
