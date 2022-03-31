---
layout: post
title: HiP(Hirarchical Perceiver) review
subtitle: Hierarchical Perceiver, 2022
categories: Paper-review
tags: multi-modal-learning
comments: True
published: True
---
## Summary 
이번에 살펴본 논문은 Hierarchical Perceiver(HiP) 라는 논문입니다. 기존의 Perceiver 류의 모델이 Transformer 기반의 모델 구조, cross attention을 통해 다양한 modality를 다룰 수 있었습니다. 한편, High resolution을 가진 Image, Video 등의 입력에 대해서는 처리가 어려운 문제점을 지적합니다. 따라서 그에 대한 해결책으로 Hierarchical Perceiver(이하 HiP)를 제안합니다. HiP에서는 flatten operation을 통해서 input을 각 그룹으로 나누어, locality를 보존시키며 연산을 수행합니다. 각 그룹은 permutation invariant한 특성을 이용해 다시 merge하게 됩니다. 또한 large input에 대해서도 dense low-dimensional position embedding을 학습하기 위해 Masked Auto Encoding(MAE) self-supervied learning을 활용합니다. <a href = "https://arxiv.org/pdf/2111.06377.pdf">Masked Autoencoders Are Scalable Vision Learners</a> 논문에서 제시한 <b>"masking을 활용한 pretrain이 여러 finetuning task에 효율적이다."</b>라는 점을 본 논문에서도 학습에 활용하였습니다. 이를 통해 ImageNet, Audioset, PASCAL VOC 에서 기존의 Perceiver 대비 더 나은 정확도와 효율성을 보이고 있습니다.
## Main Idea
![fig](/assets/images/hirarchical-perceiver/fig2.jpg)
<br>
위 사진의 왼쪽 그림은 기본적인 HiP 블록에 대한 구조를 보여줍니다. large size inputd에 대해 locality를 보존하기 위해서 flattening을 사용하고 있습니다. flattening은 large 입력에 대해서 순서대로 특정 size만큼 잘라서 stack 형식으로 쌓기 때문에 어느 정도의 locality가 보존되는 특성이 있습니다. 본 모델에서는 이용해 G 개의 group으로 나누어 local input에 대해 나누어 연산하고 추후 merge를 수행합니다. Transformer의 attention 연산은 input token에 대해 invariant한 특성이 있기 때문에 이러한 과정이 valid 합니다.
<br>
각 그룹에서는 M/G tokens, C channels 로 구성되어 Perceiver 의 모델구조와 동일하게 encoding(local input과 latent vector의 cross attention), processing(응축된 latent vector의 self attnetion), merge(local process 값들을 merge) 과정을 수행해 줍니다. merge된 출력 값은 next block의 입력으로 활용됩니다.
<br>
오른쪽 그림은 4-2-1-2-4 group의 hierarchical 한 구조를 잘 보여주기 위한 모식도입니다. 각각 grouping이 4개 group, 2개 group, 1개 group에서 다시 2개 gorup, 4개 group, output으로 복원의 구조를 보여줍니다.
<br>

<b>- Laerned low-dimensional positional embeddings</b>
![fig](/assets/images/hirarchical-perceiver/fig3.jpg)
<br>
위의 이미지는 왼쪽부터 순서대로 원본 이미지, 85% 비율의 groupwise-masking 이미지, 16-group model을 통한 output 복원 이미지를 나타냅니다. input tensor에 random & uniform mask 처리를 하고, decoder를 통해 나온 출력이 가려진 부분을 맞추는 식으로 positional embedding을 학습합니다. pretrain 과정은 <a href = "https://arxiv.org/pdf/2111.06377.pdf">Masked Autoencoders Are Scalable Vision Learners</a> 의 부분과 유사하게 진행되며, masking rate, hyperparameter 부분은 HiP setting에 맞게 수정하여 학습하였습니다.

## Experiements 


## Reference

## The End 






<!-- ![fig](/assets/images/hirarchical-perceiver/table1.jpg)
<br>

![fig](/assets/images/hirarchical-perceiver/table2.jpg)
<br>

![fig](/assets/images/hirarchical-perceiver/fig4.jpg)
<br> -->
