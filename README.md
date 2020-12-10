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
git clone https://github.com/dbolya/yolact.git
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

```
I seperate the original training data (33402 images) into two part. One for training (30000 images) and one for evaluating(3402 images). 

## Training
To train models:

```
cd /path/to/your/darknet/
1. pretrain:
./darknet detector train cfg/my.data cfg/yolov4.cfg yolov4.weights -dont_show -mjpeg_port 8090 -map -clear -gpus 0
2. no pretrain:
./darknet detector train cfg/my.data cfg/yolov4.cfg -dont_show -mjpeg_port 8090 -map -clear -gpus 0
```

you can see the training loss: http://localhost:8090/

The expected training times are:
Model | GPUs | Image size | Training Iteration | Training Time
------------ | ------------- | ------------- | ------------- | -------------
darknet | 1x RTX 2080Ti | 608 x 608 | 67000 | 24 hours


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
