# Visual-Recognition-HW3
NCTU Visual Recognition Homework 3 (YOLOv4 C++ ver.)

## Hardware
OS: Ubuntu 18.04.3 LTS

CPU: Intel(R) Xeon(R) W-2133 CPU @ 3.60GHz

GPU: 2x GeForce RTX 2080 TI

## Reproducing Submission
To reproduct my submission without retrainig, do the following steps:
1. [Installation](#installation)
2. [Dataset Preparation](#Dataset-Preparation)
3. [Training detail](#Training)
4. [Testing detail](#Testing)
5. [Reference](#Reference)

## Installation

this code was trained and tested on Ubuntu 18.04

```
conda env create -f environment.yml

```

## Dataset Preparation
```
cs-t0828-2020-hw3

├── HW3
│   ├── yolact 
│   │   ├── test_images
│   │   │   ├── Put testing images here
│   │   ├── test.json
│   │   ├── sbd
│   │   │   ├── img
│   │   │   │   ├── Put training and validation images here
│   │   │   ├── pascal_sbd_train.json
│   │   │   ├── pascal_sbd_val.json
│   ├── weights
│   │   ├── Put pretrained (Imagenet) resnet50 weight here

```
I seperate the original training data (1349 images) into two part. One for training (1200 images) and one for evaluating(149 images). 

## Training
To train models:

```
cd /path/to/your/yolact/
python train.py --config=yolact_resnet50_pascal_config --batch_size=20 --batch_alloc=10,10 --validation_epoch=4 --save_epoch=4
```

The expected training times are:
Model | GPUs | Image size | Training Epoch | Training Time
------------ | ------------- | ------------- | ------------- | -------------
darknet | 2x RTX 2080Ti | 550 x 550 | 144 | 2 hours


## Testing
To test models:

```
cd /path/to/your/darknet/
./darknet detector test cfg/my.data cfg/yolov4.cfg yolov4_20000.weights -thresh 0.001 -ext_output -dont_show -out result.json < ../../HW2/test.txt
```
[Pretrain weight](https://drive.google.com/file/d/1tMZML34PD7cvxMz7SpKit_nNA5FgVj-h/view?usp=sharing)

## Reference
1. [YOLO](https://github.com/AlexeyAB/darknet).
2. [.mat to .csv](https://github.com/pavitrakumar78/Street-View-House-Numbers-SVHN-Detection-and-Classification-using-CNN/blob/master/construct_datasets.py)
