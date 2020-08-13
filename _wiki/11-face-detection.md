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

[ParamidBox][PyramidBox]认为网络最高两层的特征由于 1）尺度太大，抽象过高；2）感受野过大，可能引入不干净的上下文信息（noisy context feature), 作者提出`LFPN` 将 [FPN][FPN] 的上采样层变为倒二层开始。


### 正负样本划分、Anchor 匹配等  

[S3FD][S3FD]: 1）将匹配阈值从0.5调降到0.35增加匹配个数， 同时2）对于匹配个数较少的人脸降低阈值到0.1， 晒全重叠度前N的 Anchor.
[HAMBox][HAMBox] 观察到， 未匹配的 Anchor 展现出很强的回归能力，很大一部分的未匹配Anchor能够回归出于真值人脸重叠度非常高的框。基于这个观察，作者在训练中对这部分Anchor进行补偿， 即将这一部分中质量较高的框纳入正样本和回归的范畴

### 数据增益方法

[ParamidBox][PyramidBox] 提出 **Data-anchor-sampling**: 对于每张图片，随机从中选取一张人脸， 根据大小得到尺寸最接近的 anchor。 再从最小的 anchor 和 两倍这个anchor之间随机选取一个anchor， 用这个anchor作为选取的人脸要缩放的目标大小。根据这个缩放系数，将图片进行缩放， 在裁剪出网络需要的输入大小。该增益方式趋向于将选取的人脸往小的方向进行缩放，有利于将提高小人脸的占比，同时将大人脸变小，提高了小人连的多样性。

[DSFD][DSFD]

[S3FD]: https://arxiv.org/abs/1708.05237
[HAMBox]: https://openaccess.thecvf.com/content_CVPR_2020/papers/Liu_HAMBox_Delving_Into_Mining_High-Quality_Anchors_on_Face_Detection_CVPR_2020_paper.pdf
[PyramidBox]: https://arxiv.org/pdf/1803.07737.pdf
[FPN]: https://arxiv.org/abs/1612.03144
[DSFD]: http://arxiv.org/abs/1810.10220

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
- Xuepeng Shi, Shiguang Shan, Meina Kan, Shuzhe Wu, Xilin Chen .[Real-Time Rotation-Invariant Face Detection with Progressive Calibration  Networks](https://arxiv.org/pdf/1804.06039) .[J] arXiv preprint arXiv:1804.06039.<br>[code:[Jack-CV/FaceKit](https://github.com/Jack-CV/FaceKit)]
- Jianfeng Wang, Ye Yuan, Boxun Li, Gang Yu, Sun Jian .[SFace: An Efficient Network for Face Detection in Large Scale Variations](https://arxiv.org/pdf/1804.06559) .[J] arXiv preprint arXiv:1804.06559.
- Yuqian Zhou, Ding Liu, Thomas Huang .[Survey of Face Detection on Low-quality Images](https://arxiv.org/pdf/1804.07362) .[J] arXiv preprint arXiv:1804.07362.
- Hajime Nada, Vishwanath A. Sindagi, He Zhang, Vishal M. Patel .[Pushing the Limits of Unconstrained Face Detection: a Challenge Dataset  and Baseline Results](https://arxiv.org/pdf/1804.10275) .[J] arXiv preprint arXiv:1804.10275.<br>[code:[ufdd.info](https://ufdd.info/)]
- 【.】Ce Qi, Xiaoping Chen, Pingyu Wang, Fei Su .[Precise Box Score: Extract More Information from Datasets to Improve the  Performance of Face Detection](https://arxiv.org/pdf/1804.10743) .[J] arXiv preprint arXiv:1804.10743.
- Baosheng Yu, Dacheng Tao .[Anchor Cascade for Efficient Face Detection](https://arxiv.org/pdf/1805.03363) .[J] arXiv preprint arXiv:1805.03363.
- Mehmet Kerim Yucel, Yunus Can Bilge, Oguzhan Oguz, Nazli Ikizler-Cinbis, Pinar Duygulu, Ramazan Gokberk Cinbis .[Wildest Faces: Face Detection and Recognition in Violent Settings](https://arxiv.org/pdf/1805.07566) .[J] arXiv preprint arXiv:1805.07566.
- Avishek Joey Bose, Parham Aarabi .[Adversarial Attacks on Face Detectors using Neural Net based Constrained  Optimization](https://arxiv.org/pdf/1805.12302) .[J] arXiv preprint arXiv:1805.12302.
- Yuezun Li, Ming-Ching Chang, Siwei Lyu .[In Ictu Oculi: Exposing AI Generated Fake Face Videos by Detecting Eye  Blinking](https://arxiv.org/pdf/1806.02877) .[J] arXiv preprint arXiv:1806.02877.
- Gustavo Botelho de Souza, João Paulo Papa, Aparecido Nilceu Marana .[On the Learning of Deep Local Features for Robust Face Spoofing  Detection](https://arxiv.org/pdf/1806.07492) .[J] arXiv preprint arXiv:1806.07492.
- Shervin Rahimzadeh Arashloo, Josef Kittler .[Client-Specific Anomaly Detection for Face Presentation Attack Detection](https://arxiv.org/pdf/1807.00848) .[J] arXiv preprint arXiv:1807.00848.
- Moritz Lode, Michael Örtl, Christian Koch, Amr Rizk, Ralf Steinmetz .[Detection and Analysis of Content Creator Collaborations in YouTube  Videos using Face- and Speaker-Recognition](https://arxiv.org/pdf/1807.02020) .[J] arXiv preprint arXiv:1807.02020.
- Clemens Seibold, Anna Hilsmann, Peter Eisert .[Reflection Analysis for Face Morphing Attack Detection](https://arxiv.org/pdf/1807.02030) .[J] arXiv preprint arXiv:1807.02030.
- Xiao Song, Xu Zhao, Liangji Fang, Tianwei Lin .[Discriminative Representation Combinations for Accurate Face Spoofing  Detection](https://arxiv.org/pdf/1808.08802) .[J] arXiv preprint arXiv:1808.08802.
- Cheng Chi, Shifeng Zhang, Junliang Xing, Zhen Lei, Stan Z. Li, Xudong Zou .[Selective Refinement Network for High Performance Face Detection](https://arxiv.org/pdf/1809.02693) .[J] arXiv preprint arXiv:1809.02693.
- Le Thanh Nguyen-Meidine, Eric Granger, Madhu Kiran, Louis-Antoine Blais-Morin .[A Comparison of CNN-based Face and Head Detectors for Real-Time Video  Surveillance Applications](https://arxiv.org/pdf/1809.03336) .[J] arXiv preprint arXiv:1809.03336.
- Bruna Vieira Frade, Erickson R. Nascimento .[A Two-Step Learning Method For Detecting Landmarks on Faces From  Different Domains](https://arxiv.org/pdf/1809.04621) .[J] arXiv preprint arXiv:1809.04621.
- Rajeev Ranjan, Ankan Bansal, Jingxiao Zheng, Hongyu Xu, Joshua Gleason, Boyu Lu, Anirudh Nanduri, Jun-Cheng Chen, Carlos D. Castillo, Rama Chellappa .[A Fast and Accurate System for Face Detection, Identification, and  Verification](https://arxiv.org/pdf/1809.07586) .[J] arXiv preprint arXiv:1809.07586.
- Chih-Chung Hsu, Chia-Yen Lee, Yi-Xiu Zhuang .[Learning to Detect Fake Face Images in the Wild](https://arxiv.org/pdf/1809.08754) .[J] arXiv preprint arXiv:1809.08754.
- 【DSFD】Jian Li, Yabiao Wang, Changan Wang, Ying Tai, Jianjun Qian, Jian Yang, Chengjie Wang, Jilin Li, Feiyue Huang .[DSFD: Dual Shot Face Detector](https://arxiv.org/pdf/1810.10220) .[J] arXiv preprint arXiv:1810.10220.<br>[code:[TencentYoutuResearch/FaceDetection-DSFD](https://github.com/TencentYoutuResearch/FaceDetection-DSFD)]
- Yuezun Li, Siwei Lyu .[Exposing DeepFake Videos By Detecting Face Warping Artifacts](https://arxiv.org/pdf/1811.00656) .[J] arXiv preprint arXiv:1811.00656.
- Wanxin Tian, Zixuan Wang, Haifeng Shen, Weihong Deng, Binghui Chen, Xiubao Zhang .[Learning Better Features for Face Detection with Feature Fusion and Segmentation Supervision](https://arxiv.org/pdf/1811.08557) .[J] arXiv preprint arXiv:1811.08557.
- Petru Soviany, Radu Tudor Ionescu .[Continuous Trade-off Optimization between Fast and Accurate Deep Face Detectors](https://arxiv.org/pdf/1811.11582) .[J] arXiv preprint arXiv:1811.11582.
- Zhishuai Zhang, Wei Shen, Siyuan Qiao, Yan Wang, Bo Wang, Alan Yuille .[Robust Face Detection via Learning Small Faces on Hard Images](https://arxiv.org/pdf/1811.11662) .[J] arXiv preprint arXiv:1811.11662.<br>[code:[bairdzhang/smallhardface](https://github.com/bairdzhang/smallhardface)]
- Thibaut Issenhuth, Vinkle Srivastav, Afshin Gangi, Nicolas Padoy .[Face Detection in the Operating Room: Comparison of State-of-the-art Methods and a Self-supervised Approach](https://arxiv.org/pdf/1811.12296) .[J] arXiv preprint arXiv:1811.12296.
- Mingyu Ding, An Zhao, Zhiwu Lu, Tao Xiang, Ji-Rong Wen .[Face-Focused Cross-Stream Network for Deception Detection in Videos](https://arxiv.org/pdf/1812.04429) .[J] arXiv preprint arXiv:1812.04429.
- Mahyar Najibi, Bharat Singh, Larry S. Davis .[FA-RPN: Floating Region Proposals for Face Detection](https://arxiv.org/pdf/1812.05586) .[J] arXiv preprint arXiv:1812.05586.
- 【Dataset】Jian Han, Sezer Karaoglu, Hoang-An Le, Theo Gevers .[Improving Face Detection Performance with 3D-Rendered Synthetic Data](https://arxiv.org/pdf/1812.07363) .[J] arXiv preprint arXiv:1812.07363.
- Shi Luo, Xiongfei Li, Rui Zhu, Xiaoli Zhang .[SFA: Small Faces Attention Face Detector](https://arxiv.org/pdf/1812.08402) .[J] arXiv preprint arXiv:1812.08402.
- Guido Borghi .[Combining Deep and Depth: Deep Learning and Face Depth Maps for Driver Attention Monitoring](https://arxiv.org/pdf/1812.05831) .[J] arXiv preprint arXiv:1812.05831.

### 2017
- Smriti Tikoo, Nitin Malik .[Detection of Face using Viola Jones and Recognition using Back  Propagation Neural Network](https://arxiv.org/pdf/1701.08257) .[J] arXiv preprint arXiv:1701.08257.
- Smriti Tikoo, Nitin Malik .[Detection, Segmentation and Recognition of Face and its Features Using  Neural Network](https://arxiv.org/pdf/1701.08259) .[J] arXiv preprint arXiv:1701.08259.
- Xudong Sun, Pengcheng Wu, Steven C.H. Hoi .[Face Detection using Deep Learning: An Improved Faster RCNN Approach](https://arxiv.org/pdf/1701.08289) .[J] arXiv preprint arXiv:1701.08289.
- Shuo Yang, Ping Luo, Chen Change Loy, Xiaoou Tang .[Faceness-Net: Face Detection through Deep Facial Part Responses](https://arxiv.org/pdf/1701.08393) .[J] arXiv preprint arXiv:1701.08393.
- Yuguang Liu, Martin D. Levine .[Multi-Path Region-Based Convolutional Neural Network for Accurate  Detection of Unconstrained "Hard Faces"](https://arxiv.org/pdf/1703.09145) .[J] arXiv preprint arXiv:1703.09145.
- Liying Chi, Hongxin Zhang, Mingxiu Chen .[End-To-End Face Detection and Recognition](https://arxiv.org/pdf/1703.10818) .[J] arXiv preprint arXiv:1703.10818.
- Upal Mahbub, Sayantan Sarkar, Rama Chellappa .[Partial Face Detection in the Mobile Domain](https://arxiv.org/pdf/1704.02117) .[J] arXiv preprint arXiv:1704.02117.
- Zhen-Hua Feng, Josef Kittler, Muhammad Awais, Patrik Huber, Xiao-Jun Wu .[Face Detection, Bounding Box Aggregation and Pose Estimation for Robust  Facial Landmark Localisation in the Wild](https://arxiv.org/pdf/1705.02402) .[J] arXiv preprint arXiv:1705.02402.<br>[code url in paper:[dlib.net](http://dlib.net/)]
- 【Face R-CNN】【Tencent AI Lab】Hao Wang, Zhifeng Li, Xing Ji, Yitong Wang .[Face R-CNN](https://arxiv.org/pdf/1706.01061) .[J] arXiv preprint arXiv:1706.01061. 
- Shuo Yang, Yuanjun Xiong, Chen Change Loy, Xiaoou Tang .[Face Detection through Scale-Friendly Deep Convolutional Networks](https://arxiv.org/pdf/1706.02863) .[J] arXiv preprint arXiv:1706.02863.
- Zekun Hao, Yu Liu, Hongwei Qin, Junjie Yan, Xiu Li, Xiaolin Hu .[Scale-Aware Face Detection](https://arxiv.org/pdf/1706.09876) .[J] arXiv preprint arXiv:1706.09876.
- Yancheng Bai, Bernard Ghanem .[Multi-Branch Fully Convolutional Network for Face Detection](https://arxiv.org/pdf/1707.06330) .[J] arXiv preprint arXiv:1707.06330.
- Keke He, Yanwei Fu, Xiangyang Xue .[A Jointly Learned Deep Architecture for Facial Attribute Analysis and  Face Detection in the Wild](https://arxiv.org/pdf/1707.08705) .[J] arXiv preprint arXiv:1707.08705.
- Weilin Cong, Sanyuan Zhao, Hui Tian, Jianbing Shen .[Improved Face Detection and Alignment using Cascade Deep Convolutional  Network](https://arxiv.org/pdf/1707.09364) .[J] arXiv preprint arXiv:1707.09364.
- 【Focal loss】Lin T Y, Goyal P, Girshick R, et al. [Focal loss for dense object detection](https://arxiv.org/abs/1708.02002)[J]. IEEE transactions on pattern analysis and machine intelligence, 2018.<br>[code:[facebookresearch/Detectron](https://github.com/facebookresearch/Detectron)]
- Manuel Günther, Peiyun Hu, Christian Herrmann, Chi Ho Chan, Min Jiang, Shufan Yang, Akshay Raj Dhamija, Deva Ramanan, Jürgen Beyerer, Josef Kittler, Mohamad Al Jazaery, Mohammad Iqbal Nouyed, Guodong Guo, Cezary Stankiewicz, Terrance E. Boult .[Unconstrained Face Detection and Open-Set Face Recognition Challenge](https://arxiv.org/pdf/1708.02337) .[J] arXiv preprint arXiv:1708.02337.<br>[code url in paper:[pypi/challenge.uccs](http://pypi.python.org/pypi/challenge.uccs); [vast.uccs.edu/Opensetface](http://vast.uccs.edu/Opensetface); [nist.gov/face-recognition-vendor-test-frvt](https://www.nist.gov/programs-projects/face-recognition-vendor-test-frvt)]
- 【SSH】Mahyar Najibi, Pouya Samangouei, Rama Chellappa, Larry Davis .[SSH: Single Stage Headless Face Detector](https://arxiv.org/pdf/1708.03979) .[J] arXiv preprint arXiv:1708.03979.<br>[code:[mahyarnajibi/SSH](https://github.com/mahyarnajibi/SSH)]
- Nataniel Ruiz, James M. Rehg .[Dockerface: an Easy to Install and Use Faster R-CNN Face Detector in a  Docker Container](https://arxiv.org/pdf/1708.04370) .[J] arXiv preprint arXiv:1708.04370.<br>[code:[natanielruiz/dockerface](https://github.com/natanielruiz/dockerface)]
- 【FaceBoxes】Shifeng Zhang, Xiangyu Zhu, Zhen Lei, Hailin Shi, Xiaobo Wang, Stan Z. Li .[FaceBoxes: A CPU Real-time Face Detector with High Accuracy](https://arxiv.org/pdf/1708.05234) .[J] arXiv preprint arXiv:1708.05234.<br>[code:[sfzhang15/FaceBoxes](https://github.com/sfzhang15/FaceBoxes);[zeusees/FaceBoxes](https://github.com/zeusees/FaceBoxes)]
- 【S^3FD】Shifeng Zhang, Xiangyu Zhu, Zhen Lei, Hailin Shi, Xiaobo Wang, Stan Z. Li .[S^3FD: Single Shot Scale-invariant Face Detector](https://arxiv.org/pdf/1708.05237) .[J] arXiv preprint arXiv:1708.05237.<br>[code:[sfzhang15/SFD](https://github.com/sfzhang15/SFD)]
- SouYoung Jin, Hang Su, Chris Stauffer, Erik Learned-Miller .[End-to-end Face Detection and Cast Grouping in Movies Using  Erdős-Rényi Clustering](https://arxiv.org/pdf/1709.02458) .[J] arXiv preprint arXiv:1709.02458.<br>[code:[souyoungjin.com/erclustering](http://souyoungjin.com/erclustering)]
- Yujia Chen, Lingxiao Song, Ran He .[Masquer Hunter: Adversarial Occlusion-aware Face Detection](https://arxiv.org/pdf/1709.05188) .[J] arXiv preprint arXiv:1709.05188.
- 【face R-FCN】Yitong Wang, Xing Ji, Zheng Zhou, Hao Wang, Zhifeng Li .[Detecting Faces Using Region-based Fully Convolutional Networks](https://arxiv.org/pdf/1709.05256) .[J] arXiv preprint arXiv:1709.05256.
- Mahmoud Afifi, Marwa Nasser, Mostafa Korashy, Katherine Rohde, Aly Abdelrahim .[Can We Boost the Power of the Viola-Jones Face Detector Using  Pre-processing? An Empirical Study](https://arxiv.org/pdf/1709.07720) .[J] arXiv preprint arXiv:1709.07720.
- Luiz Souza, Mauricio Pamplona, Luciano Oliveira, João Papa .[How far did we get in face spoofing detection?](https://arxiv.org/pdf/1710.09868) .[J] arXiv preprint arXiv:1710.09868.
- 【FAN】Jianfeng Wang, Ye Yuan, Gang Yu .[Face Attention Network: An Effective Face Detector for the Occluded  Faces](https://arxiv.org/pdf/1711.07246) .[J] arXiv preprint arXiv:1711.07246.
- Jialiang Zhang, Xiongwei Wu, Jianke Zhu, Steven C.H. Hoi .[Feature Agglomeration Networks for Single Stage Face Detection](https://arxiv.org/pdf/1712.00721) .[J] arXiv preprint arXiv:1712.00721.
- Zexun Zhou, Zhongshi He, Ziyu Chen, Yuanyuan Jia, Haiyan Wang, Jinglong Du, Dingding Chen .[FHEDN: A based on context modeling Feature Hierarchy Encoder-Decoder  Network for face detection](https://arxiv.org/pdf/1712.03687) .[J] arXiv preprint arXiv:1712.03687.
- Siqi Yang, Arnold Wiliem, Shaokang Chen, Brian C. Lovell .[Using LIP to Gloss Over Faces in Single-Stage Face Detection Networks](https://arxiv.org/pdf/1712.08263) .[J] arXiv preprint arXiv:1712.08263.

### 2016
- Qin H, Yan J, Li X, et al. [Joint training of cascaded cnn for face detection](http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Qin_Joint_Training_of_CVPR_2016_paper.pdf)[C]//Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2016: 3456-3465.
- Michael J. Wilber, Vitaly Shmatikov, Serge Belongie .[Can we still avoid automatic face detection?](https://arxiv.org/pdf/1602.04504) .[J] arXiv preprint arXiv:1602.04504.
- Sayantan Sarkar, Vishal M. Patel, Rama Chellappa .[Deep Feature-based Face Detection on Mobile Devices](https://arxiv.org/pdf/1602.04868) .[J] arXiv preprint arXiv:1602.04868.
- Rajeev Ranjan, Vishal M. Patel, Rama Chellappa .[HyperFace: A Deep Multi-task Learning Framework for Face Detection,  Landmark Localization, Pose Estimation, and Gender Recognition](https://arxiv.org/pdf/1603.01249) .[J] arXiv preprint arXiv:1603.01249.
- Upal Mahbub, Vishal M. Patel, Deepak Chandra, Brandon Barbello, Rama Chellappa .[Partial Face Detection for Continuous Authentication](https://arxiv.org/pdf/1603.09364) .[J] arXiv preprint arXiv:1603.09364.
- 【MTCNN】Kaipeng Zhang, Zhanpeng Zhang, Zhifeng Li, Yu Qiao .[Joint Face Detection and Alignment using Multi-task Cascaded  Convolutional Networks](https://arxiv.org/pdf/1604.02878) .[J] arXiv preprint arXiv:1604.02878.<br>[code;[kpzhang93/MTCNN_face_detection_alignment](https://github.com/kpzhang93/MTCNN_face_detection_alignment)]
- Yunzhu Li, Benyuan Sun, Tianfu Wu, Yizhou Wang .[Face Detection with End-to-End Integration of a ConvNet and a 3D Model](https://arxiv.org/pdf/1606.00850) .[J] arXiv preprint arXiv:1606.00850.<br>[code:[tfwu/FaceDetectionConvNet-3D](https://github.com/tfwu/FaceDetectionConvNet-3D)]
- Huaizu Jiang, Erik Learned-Miller .[Face Detection with the Faster R-CNN](https://arxiv.org/pdf/1606.03473) .[J] arXiv preprint arXiv:1606.03473.
- Chenchen Zhu, Yutong Zheng, Khoa Luu, Marios Savvides .[CMS-RCNN: Contextual Multi-Scale Region-based CNN for Unconstrained Face  Detection](https://arxiv.org/pdf/1606.05413) .[J] arXiv preprint arXiv:1606.05413.
- Dong Chen, Gang Hua, Fang Wen, Jian Sun .[Supervised Transformer Network for Efficient Face Detection](https://arxiv.org/pdf/1607.05477) .[J] arXiv preprint arXiv:1607.05477.
- Yu J, Jiang Y, Wang Z, et al. [UnitBox: An Advanced Object Detection Network](https://arxiv.org/pdf/1608.01471)[J]. arXiv preprint arXiv:1608.01471, 2016.
- Michael McCoyd, David Wagner .[Spoofing 2D Face Detection: Machines See People Who Aren't There](https://arxiv.org/pdf/1608.02128) .[J] arXiv preprint arXiv:1608.02128.
- Shaohua Wan, Zhijun Chen, Tao Zhang, Bo Zhang, Kong-kat Wong .[Bootstrapping Face Detection with Hard Negative Examples](https://arxiv.org/pdf/1608.02236) .[J] arXiv preprint arXiv:1608.02236.
- Michael Opitz, Georg Waltner, Georg Poier, Horst Possegger, Horst Bischof .[Grid Loss: Detecting Occluded Faces](https://arxiv.org/pdf/1609.00129) .[J] arXiv preprint arXiv:1609.00129.
- Xianxu Hou, Ke Sun, Linlin Shen, Guoping Qiu .[Object Specific Deep Learning Feature and Its Application to Face  Detection](https://arxiv.org/pdf/1609.01366) .[J] arXiv preprint arXiv:1609.01366.
- Zhenheng Yang, Ram Nevatia .[A Multi-Scale Cascade Fully Convolutional Network Face Detector](https://arxiv.org/pdf/1609.03536) .[J] arXiv preprint arXiv:1609.03536.
- Shuzhe Wu, Meina Kan, Zhenliang He, Shiguang Shan, Xilin Chen .[Funnel-Structured Cascade for Multi-View Face Detection with  Alignment-Awareness](https://arxiv.org/pdf/1609.07304) .[J] arXiv preprint arXiv:1609.07304.
- Jyothi Korra .[Comparing Face Detection and Recognition Techniques](https://arxiv.org/pdf/1610.04575) .[J] arXiv preprint arXiv:1610.04575.
- Zhuqi Li, Weijie Chen, Zhenyi Li, Kaigui Bian .[Look into My Eyes: Fine-grained Detection of Face-screen Distance on  Smartphones](https://arxiv.org/pdf/1612.04131) .[J] arXiv preprint arXiv:1612.04131.
- 【HR】Peiyun Hu, Deva Ramanan .[Finding Tiny Faces](https://arxiv.org/pdf/1612.04402) .[J] arXiv preprint arXiv:1612.04402.<br>[code: [peiyunh/tiny](https://github.com/peiyunh/tiny)]
- Yutong Zheng, Chenchen Zhu, Khoa Luu, Chandrasekhar Bhagavatula, T. Hoang Ngan Le, Marios Savvides .[Towards a Deep Learning Framework for Unconstrained Face Detection](https://arxiv.org/pdf/1612.05322) .[J] arXiv preprint arXiv:1612.05322.


### 2015
- 【Cascade】Li H, Lin Z, Shen X, et al. [A convolutional neural network cascade for face detection](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Li_A_Convolutional_Neural_2015_CVPR_paper.pdf)[C]//Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2015: 5325-5334.<br>[code:[anson0910/CNN_face_detection](https://github.com/anson0910/CNN_face_detection)]
- Yang B, Yan J, Lei Z, et al. [Convolutional channel features](https://www.cv-foundation.org/openaccess/content_iccv_2015/papers/Yang_Convolutional_Channel_Features_ICCV_2015_paper.pdf)[C]//Proceedings of the IEEE international conference on computer vision. 2015: 82-90.<br>[code:[bitbucket.org/binyangderek/ccf](https://bitbucket.org/binyangderek/ccf)]
- 【Multiview Face Detection】Sachin Sudhakar Farfade, Mohammad Saberian, Li-Jia Li .[Multi-view Face Detection Using Deep Convolutional Neural Networks](https://arxiv.org/pdf/1502.02766) .[J] arXiv preprint arXiv:1502.02766.<br>[code: [guoyilin/FaceDetection_CNN](https://github.com/guoyilin/FaceDetection_CNN)]
- Anjith George, Anirban Dasgupta, Aurobinda Routray .[A Framework for Fast Face and Eye Detection](https://arxiv.org/pdf/1505.03344) .[J] arXiv preprint arXiv:1505.03344.
- Golnaz Ghiasi, Charless C. Fowlkes .[Occlusion Coherence: Detecting and Localizing Occluded Faces](https://arxiv.org/pdf/1506.08347) .[J] arXiv preprint arXiv:1506.08347.
- Ilya Kalinovskii, Vladimir Spitsyn .[Compact Convolutional Neural Network Cascade for Face Detection](https://arxiv.org/pdf/1508.01292) .[J] arXiv preprint arXiv:1508.01292.
- Rajeev Ranjan, Vishal M. Patel, Rama Chellappa .[A Deep Pyramid Deformable Part Model for Face Detection](https://arxiv.org/pdf/1508.04389) .[J] arXiv preprint arXiv:1508.04389.<br>[code:[fddb/results](http://vis-www.cs.umass.edu/fddb/results.html)]
- From Facial Parts Responses to Face Detection: A Deep Learning Approach [Online](http://arxiv.org/abs/1509.06451)
- WIDER FACE: A Face Detection Benchmark [Online](http://arxiv.org/abs/1511.06523)




