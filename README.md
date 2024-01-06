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