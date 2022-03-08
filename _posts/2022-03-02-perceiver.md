---
layout: post
title: Perceiver review
subtitle: Perceiver, General Perception with Iterative Attention, 2021
categories: Paper-review
tags: multi-modal-learning
comments: True
published: False
---

## Summary 
이번에 읽어본 논문은 <a href=https://arxiv.org/abs/2103.03206> Percevier: General Perception with Iterative Attention</a> 입니다. Perceiver는 다양한 data modality를 다루기 위한 새로운 model architecture를 제안합니다. domain specific assumption 을 줄이기 위해 많은 고민을 한 논문이라는 생각이 듭니다. 가장 인상깊었던 부분은 image input에 대해 2D conv 같은 preprocess 없이 약 50,000 pixel에 직접적으로 attending 합니다. (conv를 사용하게 되면 locally inductive bias 를 가지게 되는데요, general model을 다루기 위한 부분에서 이런 모델의 자체적인(?) additional assumption을 최소화하기 위해 사용을 피한 것처럼 보입니다.) 모델은 기본적으로 Transformer module 을 활용한 구조로 이루어지며, asymmetric cross attention 을 통해 model complexity를 줄이고, latent Transformer 를 활용합니다. 또 position encoding 을 위해 Fourier Feature를 활용한 방법을 사용합니다.결과적으로 images, point clouds, audio, video, and video+audio 등의 다양한 modality 에 대한 classification task에서 competitive 하거나 outperform 을 보여주고 있습니다.

## Main Idea 
![fig](/assets/images/perceiver/fig1.jpg)
<br>

## Experiments 


## 마치며