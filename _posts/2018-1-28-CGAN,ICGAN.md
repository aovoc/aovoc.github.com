---
layout: post
category : GAN
tagline: ""
tags : [GAN, DL]
---

# CGAN  

论文：  
[Conditional Generative Adversarial Nets](https://arxiv.org/pdf/1411.1784.pdf)  

github:  
[tensorflow-generative-model-collections](https://github.com/hwalsuklee/tensorflow-generative-model-collections)

## 思路  
在生成器和判别器都添加先验信息标签来条件生成指定类别的图像。


## 结构  

CGAN的结构如下：   

<img src="/assets/pics/cgan-arch.PNG" alt="结构"/>

CGAN与GAN的具体结构的对比：   

<img src="/assets/pics/cgan-arch2.PNG" alt="结构"/>



## LOSS  

gan的loss:   
 
<img src="/assets/pics/cgan-gan-loss.PNG" alt="loss"/> 

cgan的loss:

<img src="/assets/pics/cgan-loss.PNG" alt="loss"/> 

# ICGAN  

论文：
[Invertible Conditional GANs for image editing](https://arxiv.org/pdf/1611.06355.pdf)

github:
[ICGan-tensorflow](https://github.com/zhangqianhui/ICGan-tensorflow)

## 思路  

将CGAN和Encoder 结合起来，将源图像的特征向量分离改变后重新生成新图像。通过Encoder,将一幅真实的图像编码为潜在编码z和特征向量y,改变条件向量y中的特征位，重新生成源图像改变特征后得到的新图像。


## 结构   
ICGAN的结构如下：
<img src="/assets/pics/icgan-arch.PNG" alt="结构"/> 

ICGAN中CGAN的具体结构：
<img src="/assets/pics/icgan-cgan-arch.PNG" alt="结构"/> 

在生成器和判别器较早的引入了标签信息。

## 具体网络  

生成器网络：  
<img src="/assets/pics/icgan-G-network.PNG" alt="结构"/>  

判别器结构：   
<img src="/assets/pics/icgan-D-network.PNG" alt="结构"/>  

Encoder结构：  
<img src="/assets/pics/icgan-Encoder-network.PNG" alt="结构"/>  

## loss  

<img src="/assets/pics/icgan-loss1.PNG" alt="loss"/> 


## 训练过程   

IcGAN的训练包含3个步骤：   
1. 训练cGAN    
2. 用cGAN生成数据集A     
3. 用数据集A训练编码器Ez,使Ez能够将图像解析成对应的潜在编码z  
4. 用真实数据集训练生成器Z   



