---
title: "工程笔记"
permalink: /wiki/engineering/
last_modified_at: 2020-08-11
toc: true
---

## Linux  
- [Fix The Google GPG Error on Ubuntu](https://www.omgubuntu.co.uk/2017/08/fix-google-gpg-key-linux-repository-error)
- [CudaDockerFile](https://gitlab.com/nvidia/container-images/cuda/-/tree/master/dist/ubuntu18.04/10.1)

## PyTorch

### 分布式训练  
- 分布式训练相关资料  
  - [Distributed model training in PyTorch using DistributedDataParallel](https://spell.ml/blog/pytorch-distributed-data-parallel-XvEaABIAAB8Ars0e)
- 分布式训练的时候， PyTorch 时如何 reduce loss 的， 对于学习率是否需要处理？  
  PyTorch 的分布式训练在每个节点上单独进行forward， loss 和backward 计算， 然后在节点之间传递梯度，做reduce（对梯度取平均）
  所以， 分布式训练的时候， 学习率只要考虑每个节点对应的batch-size下的学习率即可， 不需要根据节点的个数缩放学习率！
  - [Should we split batch_size according to ngpu_per_node when DistributedDataparallel](https://discuss.pytorch.org/t/should-we-split-batch-size-according-to-ngpu-per-node-when-distributeddataparallel/72769)
  - [DistributedDataParallel loss compute and backpropogation?](https://discuss.pytorch.org/t/distributeddataparallel-loss-compute-and-backpropogation/47205)
- **BN 问题**  
  - [How does Dataparallel handels batch norm?](https://discuss.pytorch.org/t/how-does-dataparallel-handels-batch-norm/14040/2)
