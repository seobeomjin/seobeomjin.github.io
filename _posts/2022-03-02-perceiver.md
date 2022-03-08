---
layout: post
title: Perceiver review
subtitle: Perceiver, General Perception with Iterative Attention, 2021
categories: Paper-review
tags: multi-modal-learning
comments: True
published: True
---

## Summary 
이번에 읽어본 논문은 <a href="https://arxiv.org/abs/2103.03206"> Percevier: General Perception with Iterative Attention</a> 입니다. Perceiver는 다양한 data modality를 다루기 위한 새로운 model architecture를 제안합니다. domain specific assumption 을 줄이기 위해 많은 고민을 한 논문이라는 생각이 듭니다. 가장 인상깊었던 부분은 image input에 대해 2D conv 같은 preprocess 없이 약 50,000 pixel에 직접적으로 attending 합니다. (conv를 사용하게 되면 locally inductive bias 를 가지게 되는데요, general model을 다루기 위한 부분에서 이런 모델의 자체적인(?) additional assumption을 최소화하기 위해 사용을 피한 것처럼 보입니다.) 모델은 기본적으로 Transformer module 을 활용한 구조로 이루어지며, asymmetric cross attention 을 통해 model complexity를 줄이고, latent Transformer 를 활용합니다. 또 explicit spatial or temporal information 을 주지 않은 데에 대해서, high-fidelity Fourier Feature를 통해 보완합니다. 결과적으로 images, point clouds, audio, video, and video+audio 등의 다양한 modality 에 대한 classification task에서 competitive 하거나 outperform 을 보여주고 있습니다.

## Main Idea 
![fig](/assets/images/perceiver/fig1.jpg)
<br>
위의 그림은 Perceiver 의 모델구조를 보여줍니다. Perceiver는 domain-specific assumption이 없는 high dimensional inputs을 attentional mechanism을 통해 fixed-dimentional latent bottleneck으로 scailing합니다. 또한 그림에서 알 수 있듯이 input byte array에 iterative하게 attending하는 모습을 보여줍니다.<br>
<br>
본 모델에서 주요할 부분은 크게 2가지 입니다. 하나는 <b>cross-attention module</b>이고, 다른 하나는 latent array에서 latent array 로 mapping시키는 <b>latent transformer</b>입니다. cross-attention module에서는 asymmetric cross attention을 사용함으로써 quaduratic scailing problem을 다소 해결하는 모습을 보여줍니다.


## Experiments 


## 마치며
<!-- - 아쉬운 점 
    - cross attention 에서 bottleneck을 만들어서 complexity를 줄인 모델 구조이긴 하지만, 그렇기 때문에 all of the necessary detail 을 capture하지 못하는 문제가 있다. 그래서 그걸 capture하기 위해 itertaive attending을 해주지만, 그게 반복되면 또 computational power 가 linear 하게 (input 의 입력 횟수만큼) 증가한다. 이건 어떻게 해결할 수 있을까. -->