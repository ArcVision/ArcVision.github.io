---
layout: single
permalink: /wiki/object-detection/
toc: true
---

## 我认为

1. 在匹配的阶段，固定Anchor的长宽比是不合理的，anchor应当只表达尺度和偏移信息，而每个目标应当用其对应的长宽比的anchor进行匹配。

## 文章

- [精度45.9%，推理速度72.9FPS，百度飞桨推出工业级目标检测模型 PP-YOLO](https://mp.weixin.qq.com/s?__biz=MzIzNjc1NzUzMw==&mid=2247550882&idx=2&sn=65ad74eb647de9f47143de6306e45496&chksm=e8d0b0d0dfa739c6f92fb0513c208e34c5f7e8fa114ad4c1122602972c33e61cbd4fa4bd694d&mpshare=1&scene=1&srcid=0813mNBu8yAQIUKS5cvSgg8o&sharer_sharetime=1597298235331&sharer_shareid=b72104ff5f54bd94e90ff3fc1c88a136&version=3.0.27.2701&platform=win&rd2werd=1#wechat_redirect)
- [CNN 中的等变(equivariant)和不变(invariant)](http://www.lunarnai.cn/2018/03/23/CNN_euivariant_invariant/)

## 典型问题

### 物体旋转问题

[Oriented Object Detection in Aerial Images with Box Boundary-Aware Vector][BBA-Vectors]  
[遥感旋转目标检测方法解读（CSL, ECCV2020）](https://zhuanlan.zhihu.com/p/111493759)  
[旋转目标(遥感/文字)检测方法整理（2017-19年）](https://zhuanlan.zhihu.com/p/98703562)

[BBA-Vectors]: https://arxiv.org/pdf/2008.07043v1.pdf

## Papers


