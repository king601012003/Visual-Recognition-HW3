# Visual-Recognition-HW3
NCTU Visual Recognition Homework 3

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
cd /path/to/your/yolact/
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
│   ├── results
│   │   ├── your testing result will be here

```
I seperate the original training data (1349 images) into two part. One for training (1200 images) and one for validation(149 images). (seperate_train_val.py can seperate original pascal_train.json randomly into training and validation)



## Training
To train models:

```
cd /path/to/your/yolact/
python train.py --config=yolact_resnet50_pascal_config --batch_size=20 --batch_alloc=10,10 --validation_epoch=4 --save_epoch=4
```
[Pretrained weight resnet50 (Imagenet) ](https://drive.google.com/file/d/1xFwvDAvP2zN37oMLfV7y6UazPK7gxf93/view?usp=sharing)


The expected training times are:
Model | GPUs | Image size | Training Epoch | Training Time
------------ | ------------- | ------------- | ------------- | -------------
YOLACT | 2x RTX 2080Ti | 550 x 550 | 144 | 2 hours


## Testing
To test models:

```
cd /path/to/your/yolact/
python createJSON.py --config=yolact_resnet50_pascal_config --trained_model=/path/to/your/well-trained weight/
```
[Pretrain weight](https://drive.google.com/file/d/1wv0pt55BxV43i0CbGaUgsxYU_OzuBlIE/view?usp=sharing)

## Reference
1. [YOLACT](https://github.com/dbolya/yolact).
