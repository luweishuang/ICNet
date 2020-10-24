# **ICNet: Intra-saliency Correlation Network for Co-Saliency Detection**

This repository is the official PyTorch implementation of our *NeurIPS(2020)* paper.

You can switch the branch to "CN", to view README.md (Chinese version) and obtain codes with Chinese comments.

(您可以将 branch 切换到 "CN", 以查看中文版 README.md 并获取带有中文注释的代码)

<div align=center><img width="450" height="300" src=./thumbnail.png/></div>

## Training Datasets

**Our training set is a subset of the *COCO* dataset, containing 9213 images.**

* ***COCO9213-os.zip*** (images with original size, 4.53GB), [GoogleDrive](https://drive.google.com/file/d/1fOfSX_CtWizDapB0OeTJxAydL2yDOP5H/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1wOxdP6EQEqMwjg3_v1z2-A) (fetch code: 5183).

* ***COCO9213.zip*** (images resized to 224*224, 943MB), [GoogleDrive](https://drive.google.com/file/d/1GbA_WKvJm04Z1tR8pTSzBdYVQ75avg4f/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1r-qCLeG3L6i-OrBfKrXANg) (fetch code: 8d7z).

## Test Datasets

### Used in our paper:

* ***MSRC*** (7 groups, 233 images) ''Object Categorization by Learned Universal Visual Dictionary, *ICCV(2005)*''

* ***iCoseg*** (38 groups, 643 images) ''iCoseg: Interactive Co-segmentation with Intelligent Scribble Guidance, *CVPR(2010)*''

* ***Cosal2015*** (50 groups, 2015 images) Detection of Co-salient Objects by Looking Deep and Wide, *IJCV(2016)*''

You can download them from:

***test-datasets*** (resized to 224*224, 77MB) [GoogleDrive](https://drive.google.com/drive/folders/1bjI2msek72dOejmK796tXyjFPIE27267?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1KX7m0g9mgACoTMgkbIjRvw) (fetch code: oq5w).

***test-datasets-os*** (original sizes, 142MB) [GoogleDrive](https://drive.google.com/drive/folders/1p--uTLIF-2hRIJk9Xmys9ftTdXrWYslS?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1kDv7icEDT5pPwQQJkHkgpA) (fetch code: ujdl).

### Released recently:

* **[*CoSOD3k*](http://dpfan.net/CoSOD3K/)** (160 groups, 3316 images) ''Taking a Deeper Look at the Co-salient Object Detection, *CVPR(2020)*''

* **[*CoCA*](http://zhaozhang.net/coca.html)** (80 groups, 1295 images) ''Gradient-Induced Co-Saliency Detection, *ECCV(2020)*''

## Pre-trained Model

We provide pre-trained ICNet based on SISMs produced by pre-trained [EGNet](https://github.com/JXingZhao/EGNet) (VGG16-based).

***ICNet_vgg16.pth*** (70MB), [GoogleDrive](https://drive.google.com/file/d/1wcT_XmwlshbLqCiJetmzQwi1ZNAzxiSU/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1__iiBcAI2S-Ns9MZnZwp8g) (fetch code: nkj9).

## Prediction Results

We release the co-saliency maps (predictions) generated by our ICNet on 5 benchmark datasets:

***MSRC***, ***iCoseg***, ***Cosal2015***, ***CoCA***, and ***CoSOD3k***.

***cosal-maps.zip*** (results of size 224*224, 20MB), [GoogleDrive](https://drive.google.com/file/d/1q9CAzPf5U3VPa_DGxzUGI_DANCuw_WEk/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1qbPJKMTiVStqjSGYWuqSgQ) (fetch code: du5e).

***cosal-maps-os.zip*** (results resized to original sizes, 62MB), [GoogleDrive](https://drive.google.com/file/d/1px4tPVWAgbBPMt6Rp23oNwWz8Ulj6pmX/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1WFQxeIOjOiByiFYHLpuytA) (fetch code: xwcv).

## Training and Test

### Prepare SISMs

Our ICNet can be trained and tested based on SISMs produced by any off-the-shelf SOD method, but you are suggested to use the **same** SOD method to generate SISMs in training and test phases to keep the consistency. 

In our paper, we choose the pre-trained [EGNet](https://github.com/JXingZhao/EGNet) (VGG16-based) as the basic SOD method to produce SISMs, you can downloaded these SISMs directly from:

***EGNet-SISMs*** (resized to 224*224, 125MB) [GoogleDrive](https://drive.google.com/drive/folders/1cGtXQI2U8pH37-mgSw3otnMsRi36QwBp?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/11xJz-_TPXaL0cnwUYFUOsw) (fetch code: xc5k).

### Training

1. Download pre-trained VGG16 from:

   ***vgg16_feat.pth*** (56MB) [GoogleDrive](https://drive.google.com/file/d/1ej5ngj2NYH-R-0GfYUDfuM-DNLuFolED/view?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/1S_D6qCE2vn_okBhT1Zg72g) (fetch code: imsf).

2. Follow instructions in **"./ICNet/train.py"** to modify training settings.

3. Run:

```
python ./ICNet/train.py
```

### Test

1. * Test **pre-trained** ICNet:

     Download pre-trained ICNet ***"ICNet_vgg16.pth"*** (the download link is given above).

   * Test ICNet **trained by yourself**:

     Choose the checkpoint file ***"Weights_i.pth"***  (saved after i-th epoch automatically) you want to load for test.

2. Follow instructions in **"./ICNet/test.py"** to modify test settings.

3. Run:

```
python ./ICNet/test.py
```

## Evaluation

The folder "./ICNet/evaluator/" contains evaluation codes implemented in PyTorch (GPU-version), the metrics include **max F-measure**, **S-measure** and **MAE**. 

1. Follow instructions in **"./ICNet/evaluate.py"** to modify evaluation settings.

2. Run:

```
python ./ICNet/evaluate.py
```

## Compared Methods

We compare our ICNet with 7 state-of-the-art Co-SOD methods:

* ***CBCS***		''Cluster-Based Co-Saliency Detection, *TIP(2013)*''​			  

* ***CSHS***		''Co-Saliency Detection Based on Hierarchical Segmentation, *SPL(2014)*''

* ***CoDW***		''Detection of Co-salient Objects by Looking Deep and Wide, *IJCV(2016)*''

* ***UCSG***		''Unsupervised CNN-based Co-Saliency Detection with Graphical Optimization, *ECCV(2018)*''

* ***CSMG***		''Co-saliency Detection via Mask-guided Fully Convolutional Networks with Multi-scale Label Smoothing, *CVPR(2019)*''

* ***MGLCN***		''A Unified Multiple Graph Learning and Convolutional Network Model for Co-saliency Estimation, *ACM MM(2019)*''

* ***GICD***		''Gradient-Induced Co-Saliency Detection, *ECCV(2020)*''

You can download predictions of these methods from:

***compared_method*s** (original sizes, 445MB) [GoogleDrive](https://drive.google.com/drive/folders/1qdXWZQ-fF-WaCF-rat0Da7vFrAIYsj09?usp=sharing) | [BaiduYun](https://pan.baidu.com/s/10vpubz39atkg2lz095QvSQ) (fetch code: s7pr).

## Citation

*To be updated.*

## Contact

If you have any questions, feel free to contact me (Wen-Da Jin) at jwd331@126.com, I will reply as soon as possible.