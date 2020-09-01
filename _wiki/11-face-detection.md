---
title: "人脸检测"
permalink: /wiki/face-detection/
last_modified_at: 2020-08-08
# redirect_from:
#   - /math/
toc: true
---

## 典型问题

### 模型增强、特征融合等

[ParamidBox][ParamidBox]认为网络最高两层的特征由于 1）尺度太大，抽象过高；2）感受野过大，可能引入不干净的上下文信息（noisy context feature), 作者提出`LFPN` 将 [FPN][FPN] 的上采样层变为倒二层开始。[DSFD][DSFD] 提出`FEM`模块， 通过`dilation`卷积增加感受野， 并且上采样之后的特征融合方式改为乘法.  


### 正负样本划分、Anchor 匹配等  

[S3FD][S3FD]: 1）将匹配阈值从0.5调降到0.35增加匹配个数， 同时2）对于匹配个数较少的人脸降低阈值到0.1， 晒全重叠度前N的 Anchor.
[HAMBox][HAMBox] 观察到， 未匹配的 Anchor 展现出很强的回归能力，很大一部分的未匹配Anchor能够回归出于真值人脸重叠度非常高的框。基于这个观察，作者在训练中对这部分Anchor进行补偿， 即将这一部分中质量较高的框纳入正样本和回归的范畴

### 数据增益方法

[PyramidBox][PyramidBox] 提出 **Data-anchor-sampling**: 对于每张图片，随机从中选取一张人脸， 根据大小得到尺寸最接近的 anchor。 再从最小的 anchor 和 两倍这个anchor之间随机选取一个anchor， 用这个anchor作为选取的人脸要缩放的目标大小。根据这个缩放系数，将图片进行缩放， 在裁剪出网络需要的输入大小。该增益方式趋向于将选取的人脸往小的方向进行缩放，有利于将提高小人脸的占比，同时将大人脸变小，提高了小人连的多样性。[DSFD][DSFD] 中的 **IMA** 采用了类似的采样方式，增大人脸匹配到 anchor 的概率。

[S3FD]: https://arxiv.org/abs/1708.05237
[HAMBox]: https://openaccess.thecvf.com/content_CVPR_2020/papers/Liu_HAMBox_Delving_Into_Mining_High-Quality_Anchors_on_Face_Detection_CVPR_2020_paper.pdf
[ParamidBox]: https://arxiv.org/pdf/1803.07737.pdf
[FPN]: https://arxiv.org/abs/1612.03144
[DSFD]: http://arxiv.org/abs/1810.10220

### NMS 方法

* Non-maximum Suppression (NMS)
* Soft-NMS [[1]](https://arxiv.org/abs/1704.04503)
* Non-maximum weighted (NMW) [[2]](http://openaccess.thecvf.com/content_ICCV_2017_workshops/papers/w14/Zhou_CAD_Scale_Invariant_ICCV_2017_paper.pdf)
* **Weighted boxes fusion (WBF)** [[3]](https://arxiv.org/abs/1910.13302) - new method which gives better results comparing to others 

## 开源方案

- [Ultra-Light-Fast-Generic-Face-Detector-1MB](https://github.com/Linzaer/Ultra-Light-Fast-Generic-Face-Detector-1MB)
- [Face-Detector-1MB-with-landmark](https://github.com/biubug6/Face-Detector-1MB-with-landmark)

## 数据集与评测

- **2019** [FDDB-360：Face Detection in 360-degree Fisheye Images](https://researchdata.sfu.ca/islandora/object/sfu%3A2722)
- **2018** [4K-Face：An Efficient Network for Face Detection in Large Scale Variations](https://github.com/wjfwzzc/4K-Face)
- **2017** [Detecting Masked Faces in the Wild with LLE-CNNs(**MAFA**)](https://openaccess.thecvf.com/content_cvpr_2017/papers/Ge_Detecting_Masked_Faces_CVPR_2017_paper.pdf) 数据官网失效
- **2016** [**WIDER FACE**：A Face Detection Benchmark](http://shuoyang1213.me/WIDERFACE/)
- **2015** [Fine-grained evaluation on face detection in the wild(**MALF** )](http://www.cbsr.ia.ac.cn/faceevaluation/)
- **2011** [Annotated Facial Landmarks in the Wild (**AFLW**)](https://www.tugraz.at/institute/icg/research/team-bischof/lrs/downloads/aflw/)
- **2010** [**FDDB**: Face Detection Data Set and Benchmark](http://vis-www.cs.umass.edu/fddb/) / [Reference](http://vis-www.cs.umass.edu/fddb/fddb.pdf)

## 论文

> 中括号中内容表示简称, 不是标题的一部分

### 2020

- **ASFD**: Automatic and Scalable Face Detector [Online](http://arxiv.org/abs/2003.11228)
- **KPNet**: Towards Minimal Face Detector [Online](http://arxiv.org/abs/2003.07543)

### 2019

- **[VIM-FD]** Robust and High Performance Face Detector [Online](http://arxiv.org/abs/1901.02350)
- **DAFE-FD**: Density Aware Feature Enrichment for Face Detection [Online](http://arxiv.org/abs/1901.05375)
- **[SRN]** Improved Selective Refinement Network for Face Detection [Online](http://arxiv.org/abs/1901.06651)
- [Revisiting a single-stage method for face detection](https://arxiv.org/pdf/1902.01559)
- [FDDB-360: Face Detection in 360-degree Fisheye Images](https://arxiv.org/pdf/1902.02777)
- [Joint Face Detection and Facial Motion Retargeting for Multiple Faces](https://arxiv.org/pdf/1902.10744)
- [MSFD:Multi-Scale Receptive Field Face Detector](https://arxiv.org/pdf/1903.04147)
- [Face Detection in Repeated Settings](https://arxiv.org/pdf/1903.08649)
- [PyramidBox++: High Performance Detector for Finding Tiny Face](https://arxiv.org/pdf/1904.00386)
- [LFFD: A Light and Fast Face Detector for Edge Devices](https://arxiv.org/pdf/1904.10633)
- [Automatic cephalometric landmarks detection on frontal faces: an approach based on supervised learning techniques](https://arxiv.org/pdf/1904.10816)
- [Accelerating Proposal Generation Network for Fast Face Detection on Mobile Devices](https://arxiv.org/pdf/1904.12094)
- [Recurrent Convolutional Strategies for Face Manipulation Detection in Videos](https://arxiv.org/pdf/1905.00582)
- [RetinaFace: Single-stage Dense Face Localisation in the Wild](https://arxiv.org/pdf/1905.00641)
- [Accurate Face Detection for High Performance](https://arxiv.org/pdf/1905.01585) 
- [Detecting Bias with Generative Counterfactual Face Attribute Augmentation](https://arxiv.org/pdf/1906.06439)
- [EXTD: Extremely Tiny Face Detector via Iterative Filter Reuse](https://arxiv.org/pdf/1906.06579)
- 【Dataset】[Datasets for Face and Object Detection in Fisheye Images](https://arxiv.org/pdf/1906.11942)
- [BlazeFace: Sub-millisecond Neural Face Detection on Mobile GPUs](https://arxiv.org/pdf/1907.05047)
- [Landmark Detection in Low Resolution Faces with Semi-Supervised Learning](https://arxiv.org/pdf/1907.13255)
- [Dynamic Face Video Segmentation via Reinforcement Learning](https://arxiv.org/pdf/1907.01296)
- [RefineFace: Refinement Neural Network for High Performance Face Detection](https://arxiv.org/pdf/1909.04376)
- [On the Detection of Digital Face Manipulation](https://arxiv.org/pdf/1910.01717)
- [Complement Face Forensic Detection and Localization with FacialLandmarks](https://arxiv.org/pdf/1910.05455) 
- [Face Detection on Surveillance Images](https://arxiv.org/pdf/1910.11121)
- [Learning Structure via Consensus for Face Segmentation and Parsing](https://arxiv.org/pdf/1911.00957)
- [Face Detection in Camera Captured Images of Identity Documents under Challenging Conditions](https://arxiv.org/pdf/1911.03567)
- [DupNet: Towards Very Tiny Quantized CNN with Improved Accuracy for Face Detection](https://arxiv.org/pdf/1911.05341)
- [Face Detection with Feature Pyramids and Landmarks](https://arxiv.org/pdf/1912.00596)
- [Design and Interpretation of Universal Adversarial Patches in Face Detection](https://arxiv.org/pdf/1912.05021)
- [**HAMBox**: Delving Into Mining High-Quality Anchors on Face Detection](https://openaccess.thecvf.com/content_CVPR_2020/papers/Liu_HAMBox_Delving_Into_Mining_High-Quality_Anchors_on_Face_Detection_CVPR_2020_paper.pdf)


### 2018
- [Quality Classified Image Analysis with Application to Face Detection and  Recognition](https://arxiv.org/pdf/1801.06445)
- [Detecting and counting tiny faces](https://arxiv.org/pdf/1801.06504)
- [Face Detection Using Improved Faster RCNN](https://arxiv.org/pdf/1802.02142)
-[Detecting Anomalous Faces with 'No Peeking' Autoencoders](https://arxiv.org/pdf/1802.05798)
- [Beyond Context: Exploring Semantic Similarity for Tiny Face Detection](https://arxiv.org/pdf/1803.01555)
- [Face-MagNet: Magnifying Feature Maps to Detect Small Faces](https://arxiv.org/pdf/1803.05258) / **Code**: [po0ya/face-magnet](https://github.com/po0ya/face-magnet)]
- [Deep Adaptive Attention for Joint Facial Action Unit Detection and Face  Alignment](https://arxiv.org/pdf/1803.05588)
- [**PyramidBox**: A Context-assisted Single Shot Face Detector](https://arxiv.org/pdf/1803.07737)  / **Code**: [PaddlePaddle/face_detection](https://github.com/PaddlePaddle/models/tree/develop/fluid/face_detection)
- [A Fast Face Detection Method via Convolutional Neural Network](https://arxiv.org/pdf/1803.10103)
- [Event-based Dynamic Face Detection and Tracking Based on Activity](https://arxiv.org/pdf/1803.10106) 
- [Learning to Anonymize Faces for Privacy Preserving Action Detection](https://arxiv.org/pdf/1803.11556) / **Code**: [jason718.github.io](https://jason718.github.io/project/privacy/main.html)
- [Towards Improved Cartoon Face Detection and Recognition Systems](https://arxiv.org/pdf/1804.01753) [code url in paper:[nagadomi/animeface-2009](https://github.com/nagadomi/animeface-2009); [kaggle/facial-keypoints-detection](https://www.kaggle.com/c/facial-keypoints-detection)]
- [Beyond Trade-off: Accelerate FCN-based Face Detector with Higher  Accuracy](https://arxiv.org/pdf/1804.05197)
- [Real-Time Rotation-Invariant Face Detection with Progressive Calibration  Networks](https://arxiv.org/pdf/1804.06039) / [Code:[Jack-CV/FaceKit](https://github.com/Jack-CV/FaceKit)]
- [SFace: An Efficient Network for Face Detection in Large Scale Variations](https://arxiv.org/pdf/1804.06559)
- [Survey of Face Detection on Low-quality Images](https://arxiv.org/pdf/1804.07362)
- [Pushing the Limits of Unconstrained Face Detection: a Challenge Dataset  and Baseline Results](https://arxiv.org/pdf/1804.10275)  / [Code:[ufdd.info](https://ufdd.info/)]
- [Precise Box Score: Extract More Information from Datasets to Improve the  Performance of Face Detection](https://arxiv.org/pdf/1804.10743) 
- [Anchor Cascade for Efficient Face Detection](https://arxiv.org/pdf/1805.03363) 
- [Wildest Faces: Face Detection and Recognition in Violent Settings](https://arxiv.org/pdf/1805.07566)
- [Adversarial Attacks on Face Detectors using Neural Net based Constrained  Optimization](https://arxiv.org/pdf/1805.12302) 
- [Detection and Analysis of Content Creator Collaborations in YouTube  Videos using Face-and Speaker-Recognition](https://arxiv.org/pdf/1807.02020)
- [Selective Refinement Network for High Performance Face Detection](https://arxiv.org/pdf/1809.02693)
- [A Comparison of CNN-based Face and Head Detectors for Real-Time Video  Surveillance Applications](https://arxiv.org/pdf/1809.03336)
- [A Fast and Accurate System for Face Detection, Identification, and  Verification](https://arxiv.org/pdf/1809.07586)
- 【DSFD】[DSFD: Dual Shot Face Detector](https://arxiv.org/pdf/1810.10220) / [Code:[TencentYoutuResearch/FaceDetection-DSFD](https://github.com/TencentYoutuResearch/FaceDetection-DSFD)]
- [Learning Better Features for Face Detection with Feature Fusion and Segmentation Supervision](https://arxiv.org/pdf/1811.08557)
- [Continuous Trade-off Optimization between Fast and Accurate Deep Face Detectors](https://arxiv.org/pdf/1811.11582)
- [Robust Face Detection via Learning Small Faces on Hard Images](https://arxiv.org/pdf/1811.11662) / [Code:[bairdzhang/smallhardface](https://github.com/bairdzhang/smallhardface)]
- [Face Detection in the Operating Room: Comparison of State-of-the-art Methods and a Self-supervised Approach](https://arxiv.org/pdf/1811.12296)
- [FA-RPN: Floating Region Proposals for Face Detection](https://arxiv.org/pdf/1812.05586)
- 【Dataset】[Improving Face Detection Performance with 3D-Rendered Synthetic Data](https://arxiv.org/pdf/1812.07363) 
- [SFA: Small Faces Attention Face Detector](https://arxiv.org/pdf/1812.08402) 


### 2017
- [Detection of Face using Viola Jones and Recognition using Back  Propagation Neural Network](https://arxiv.org/pdf/1701.08257)
- [Detection, Segmentation and Recognition of Face and its Features Using  Neural Network](https://arxiv.org/pdf/1701.08259) 
- [Face Detection using Deep Learning: An Improved Faster RCNN Approach](https://arxiv.org/pdf/1701.08289)
- [Faceness-Net: Face Detection through Deep Facial Part Responses](https://arxiv.org/pdf/1701.08393)
- [Multi-Path Region-Based Convolutional Neural Network for Accurate  Detection of Unconstrained "Hard Faces"](https://arxiv.org/pdf/1703.09145) .[J] arXiv preprint arXiv:1703.09145.
- [End-To-End Face Detection and Recognition](https://arxiv.org/pdf/1703.10818) .[J] arXiv preprint arXiv:1703.10818.
-[Partial Face Detection in the Mobile Domain](https://arxiv.org/pdf/1704.02117) 
- [Face Detection, Bounding Box Aggregation and Pose Estimation for Robust  Facial Landmark Localisation in the Wild](https://arxiv.org/pdf/1705.02402)  / [code url in paper: [dlib.net](http://dlib.net/)]
- 【Face R-CNN】【Tencent AI Lab】[Face R-CNN](https://arxiv.org/pdf/1706.01061)
- [Face Detection through Scale-Friendly Deep Convolutional Networks](https://arxiv.org/pdf/1706.02863)
- [Scale-Aware Face Detection](https://arxiv.org/pdf/1706.09876) 
- [Multi-Branch Fully Convolutional Network for Face Detection](https://arxiv.org/pdf/1707.06330)
- [A Jointly Learned Deep Architecture for Facial Attribute Analysis and  Face Detection in the Wild](https://arxiv.org/pdf/1707.08705)
- [Improved Face Detection and Alignment using Cascade Deep Convolutional  Network](https://arxiv.org/pdf/1707.09364) 
- [Unconstrained Face Detection and Open-Set Face Recognition Challenge](https://arxiv.org/pdf/1708.02337) / [code url in paper: [pypi/challenge.uccs](http://pypi.python.org/pypi/challenge.uccs); [vast.uccs.edu/Opensetface](http://vast.uccs.edu/Opensetface); [nist.gov/face-recognition-vendor-test-frvt](https://www.nist.gov/programs-projects/face-recognition-vendor-test-frvt)]
- 【SSH】[SSH: Single Stage Headless Face Detector](https://arxiv.org/pdf/1708.03979)  / [code: [mahyarnajibi/SSH](https://github.com/mahyarnajibi/SSH)]
- [Dockerface: an Easy to Install and Use Faster R-CNN Face Detector in a  Docker Container](https://arxiv.org/pdf/1708.04370) / [Code: [natanielruiz/dockerface](https://github.com/natanielruiz/dockerface)]
- 【FaceBoxes】[FaceBoxes: A CPU Real-time Face Detector with High Accuracy](https://arxiv.org/pdf/1708.05234) / [Code: [sfzhang15/FaceBoxes](https://github.com/sfzhang15/FaceBoxes);[zeusees/FaceBoxes](https://github.com/zeusees/FaceBoxes)]
- 【S^3FD】[S^3FD: Single Shot Scale-invariant Face Detector](https://arxiv.org/pdf/1708.05237)  / [code:[sfzhang15/SFD](https://github.com/sfzhang15/SFD)]
- [End-to-end Face Detection and Cast Grouping in Movies Using  Erdős-Rényi Clustering](https://arxiv.org/pdf/1709.02458)  / [Code: [souyoungjin.com/erclustering](http://souyoungjin.com/erclustering)]
- [Masquer Hunter: Adversarial Occlusion-aware Face Detection](https://arxiv.org/pdf/1709.05188)
- 【face R-FCN】[Detecting Faces Using Region-based Fully Convolutional Networks](https://arxiv.org/pdf/1709.05256)
- [Can We Boost the Power of the Viola-Jones Face Detector Using  Pre-processing? An Empirical Study](https://arxiv.org/pdf/1709.07720) 
- 【FAN】[Face Attention Network: An Effective Face Detector for the Occluded  Faces](https://arxiv.org/pdf/1711.07246)
- [Feature Agglomeration Networks for Single Stage Face Detection](https://arxiv.org/pdf/1712.00721)
- [FHEDN: A based on context modeling Feature Hierarchy Encoder-Decoder  Network for face detection](https://arxiv.org/pdf/1712.03687)
- [Using LIP to Gloss Over Faces in Single-Stage Face Detection Networks](https://arxiv.org/pdf/1712.08263)

### 2016
- [Joint training of cascaded cnn for face detection](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Qin_Joint_Training_of_CVPR_2016_paper.pdf)
- [Can we still avoid automatic face detection?](https://arxiv.org/pdf/1602.04504)
- [Deep Feature-based Face Detection on Mobile Devices](https://arxiv.org/pdf/1602.04868)
- [HyperFace: A Deep Multi-task Learning Framework for Face Detection,  Landmark Localization, Pose Estimation, and Gender Recognition](https://arxiv.org/pdf/1603.01249) 
- [Partial Face Detection for Continuous Authentication](https://arxiv.org/pdf/1603.09364)
- 【MTCNN】[Joint Face Detection and Alignment using Multi-task Cascaded  Convolutional Networks](https://arxiv.org/pdf/1604.02878) / [Code: [kpzhang93/MTCNN_face_detection_alignment](https://github.com/kpzhang93/MTCNN_face_detection_alignment)]
- [Face Detection with End-to-End Integration of a ConvNet and a 3D Model](https://arxiv.org/pdf/1606.00850) / [Code: [tfwu/FaceDetectionConvNet-3D](https://github.com/tfwu/FaceDetectionConvNet-3D)]
- [Face Detection with the Faster R-CNN](https://arxiv.org/pdf/1606.03473)
- [CMS-RCNN: Contextual Multi-Scale Region-based CNN for Unconstrained Face  Detection](https://arxiv.org/pdf/1606.05413) 
- [Supervised Transformer Network for Efficient Face Detection](https://arxiv.org/pdf/1607.05477)
- [UnitBox: An Advanced Object Detection Network](https://arxiv.org/pdf/1608.01471)
- [Spoofing 2D Face Detection: Machines See People Who Aren't There](https://arxiv.org/pdf/1608.02128)
- [Bootstrapping Face Detection with Hard Negative Examples](https://arxiv.org/pdf/1608.02236) .[J] arXiv preprint arXiv:1608.02236.
- [Grid Loss: Detecting Occluded Faces](https://arxiv.org/pdf/1609.00129) .[J]
- [Object Specific Deep Learning Feature and Its Application to Face  Detection](https://arxiv.org/pdf/1609.01366)
- [A Multi-Scale Cascade Fully Convolutional Network Face Detector](https://arxiv.org/pdf/1609.03536)
- [Funnel-Structured Cascade for Multi-View Face Detection with  Alignment-Awareness](https://arxiv.org/pdf/1609.07304)
- [Comparing Face Detection and Recognition Techniques](https://arxiv.org/pdf/1610.04575) .[J] arXiv preprint arXiv:1610.04575.
- [Look into My Eyes: Fine-grained Detection of Face-screen Distance on  Smartphones](https://arxiv.org/pdf/1612.04131) 
- 【HR】[Finding Tiny Faces](https://arxiv.org/pdf/1612.04402) .[J] arXiv preprint arXiv:1612.04402. / [Code: [peiyunh/tiny](https://github.com/peiyunh/tiny)]
- [Towards a Deep Learning Framework for Unconstrained Face Detection](https://arxiv.org/pdf/1612.05322)

### 2015
- [A convolutional neural network cascade for face detection](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Li_A_Convolutional_Neural_2015_CVPR_paper.pdf) / [Code: [anson0910/CNN_face_detection](https://github.com/anson0910/CNN_face_detection)]
- [Convolutional channel features](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Yang_Convolutional_Channel_Features_ICCV_2015_paper.pdf) / [code: [bitbucket.org/binyangderek/ccf](https://bitbucket.org/binyangderek/ccf)]
- 【Multiview Face Detection】[Multi-view Face Detection Using Deep Convolutional Neural Networks](https://arxiv.org/pdf/1502.02766) / [code: [guoyilin/FaceDetection_CNN](https://github.com/guoyilin/FaceDetection_CNN)]
- [A Framework for Fast Face and Eye Detection](https://arxiv.org/pdf/1505.03344) .[J] arXiv preprint arXiv:1505.03344.
- [Occlusion Coherence: Detecting and Localizing Occluded Faces](https://arxiv.org/pdf/1506.08347)
- [Compact Convolutional Neural Network Cascade for Face Detection](https://arxiv.org/pdf/1508.01292)
- [A Deep Pyramid Deformable Part Model for Face Detection](https://arxiv.org/pdf/1508.04389) / [Code:[fddb/results](http://vis-www.cs.umass.edu/fddb/results.html)]
- From Facial Parts Responses to Face Detection: A Deep Learning Approach [Online](http://arxiv.org/abs/1509.06451)
- WIDER FACE: A Face Detection Benchmark [Online](http://arxiv.org/abs/1511.06523)




