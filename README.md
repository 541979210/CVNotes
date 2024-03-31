# 20231127

- [x] 欧拉角产生万向锁原因：欧拉角描述的是状态而非过程。

# 20231128-20240106

## transformer
### 结构
![](.\assets\transformers.png)

每个Encoder结构相同，参数不同 

![](.\assets\transformer1.png)

Encoder和Decoder结构不同

### Encoder

![](.\assets\transformer-encoder.png)
#### Embedding 

每个输入元素对应N维特征

#### 位置编码

![](.\assets\位置编码.png)

![](.\assets\位置编码1.png)
![](.\assets\位置编码2.png)

最终512维特征是位置编码与embedding相加之结果。

# 20240331

## 论文阅读：基于自适应超分的单照片驱动

### 现有难点：

1. 一些依赖几何的可微渲染/神经渲染方法通常在处理不同背景或ID时需要目标的视频进行finetune
2. 一些基于纯隐式神经渲染的方法如FOMM、TPS不需要几何先验，可以在大规模数据（如voxceleb）上进行训练，然后通过基于光流warp/jacobin矩阵变换得到驱动图像，但是其清晰度不足
3. 近期的一些工作如meta-portrait、sadtalker、videoretalking通过重新训练独立的超分模块来提升清晰度，但是两阶段的生成过程会带来额外的计算开销和误差累积

### 改进方法：

1. 融合超分方法（ESRGAN/Real-EARGAN）到端到端流程中，构建不同清晰度的图像对训练，自适应地从低质量图像中获取高频信息进行重建。

### 关键技术点：

1. 成对数据生成：源图像、驱动图像、低质量源图像、高质量驱动图像。
2. 为了避免因数据分布导致的训练与推理差异，去除了E里的BN层，有效抑制了artifacets与blurring
3. 低质量源图像和源图像送进自适应高频编码器E，源图像和驱动图像分别提取keypoints，估计motion
4. 使用SPADE模块来进行图像生成