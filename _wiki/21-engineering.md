---
title: "工程笔记"
permalink: /wiki/engineering/
last_modified_at: 2020-08-11
toc: true
---

## PyTorch

- 分布式训练相关资料  
  - [Distributed model training in PyTorch using DistributedDataParallel](https://spell.ml/blog/pytorch-distributed-data-parallel-XvEaABIAAB8Ars0e)
- 分布式训练的时候， PyTorch 时如何 reduce loss 的， 对于学习率是否需要处理？  
  PyTorch 的分布式训练在每个节点上单独进行forward， loss 和backward 计算， 然后在节点之间传递梯度，做reduce（对梯度取平均）
  所以， 分布式训练的时候， 学习率只要考虑每个节点对应的batch-size下的学习率即可， 不需要根据节点的个数缩放学习率！
  - https://discuss.pytorch.org/t/should-we-split-batch-size-according-to-ngpu-per-node-when-distributeddataparallel/72769
  - https://discuss.pytorch.org/t/distributeddataparallel-loss-compute-and-backpropogation/47205
