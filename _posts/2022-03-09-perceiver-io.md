---
layout: post
title: Perceiver IO review
subtitle: Perceiver IO, A General Architecture for Structured Inputs & Outputs, 2021
categories: Paper-review
tags: multi-modal-learning
comments: True
published: True
---

## Summary 
이번에 포스팅할 논문은 <a href = "https://arxiv.org/abs/2107.14795"> Perceiver IO: A General Architecture for Structured Inputs & Outputs </a> 입니다. Perceiver IO는 Perceiver의 출력이 단순히 classification과 같은 단순한 task에 국한되는 점을 보완하여, 다양한 structure의 Input과 Output을 가질 수 있도록 개선된 모델구조를 가지고 있습니다. (이전 포스팅은 <a href = "https://seobeomjin.github.io/paper-review/2022/03/02/perceiver.html">여기</a>를 참고해 주세요) 그 방법을 간단하게 소개하자면, <b>task별 Input에 대한 Query vector를 구성하여 Perceiver model 내부에서 얻어진 K,V 값과 사전에 구성해 둔 Query vector에 대한 cross attention을 수행하여 각 task에 맞는 size, semantic을 낼 수 있는 적절한 Output 값을 갖도록 학습합니다.</b> 그 결과 Sintel optical flow estimation task 에서는 SOTA를 달성하고, GLUE 벤치마크에서는 input tokenization 없이 BERT baseline과 유사한 성능을 보이고 있습니다.

## Main Idea 
![fig](/assets/images/perceiver-io/fig3.jpg) 
<br>
위의 그림은 Perceiver IO 의 모델구조입니다. Perceiver IO는 크게 Encoder, Process, Decoder라는 3 개의 module로 이루어진 구성입니다. Encoder에서는 Perceiver에서 large size와의 input과 cross attention을 수행하는 것과 동일하게 이루어 집니다. Process라는 과정에서도 Perceiver에서와 같이 latent Transformer를 거쳤던 것처럼 latent vector를 refine합니다. Perceiver와 달리 IO model에서는 Decode라는 부분이 새롭게 추가된 것인데요, 여기서는 latent vector에서 얻어진 K,V 값과 기존에 이미 구해둔 Output Query array를 Q로 하여 cross attention을 수행하게 됩니다. 해당 Q는 hand-desined, learned embeddings 또는 input에 대한 simple function 등으로 구성됩니다. 이러한 query vector와의 attention을 통해 적절한 shape, semantic을 가진 output을 뽑아내게 됩니다. <br>

![fig](/assets/images/perceiver-io/fig7.jpg) 
<br>
각 모듈에 대한 조금 더 상세한 과정은 위와 같습니다.

![fig](/assets/images/perceiver-io/fig4.jpg) 
<br>
위의 그림은 각 modality마다 어떤 식으로 query array가 구성되는지를 보여줍니다. MLM 같은 경우는 단순하게 position embedding 정보만 주며, classification 같은 경우는 task id를 줍니다. Starcraft2 task에서는 entities에 대한 input features가 홀로 사용되고, Optical flow task에서는 Input faeture와 position feature가 함께 사용되고 있습니다. 또, heterogeneous outputs을 다뤄야 하는 경우에는, 각각의 modality 정보가 서로 concat하여 쿼리가 만들어 집니다.


## Experiments 
#### 1. Laungage 
![fig](/assets/images/perceiver-io/fig5.jpg)
<br>
위의 Table은 GLUE benchmark 데이터셋에서 실험한 결과를 보여줍니다. (WNLI task는 제외) SenetencPiece tokenizer를 사용했을 때에는 Percevier IO모델이 아주 미세하게 조금 더 나은 성능을 보입니다. UTF-8 bytes 값을 그대로 입력으로 주었을 때에는 BERT보다 확실히 우수한 성능을 보여주는데요, 이는 본 모델의 장점으로 꼽는 tokenizer-free 한 특성을 보여주는 실험결과로 보입니다. 이를 통해 hand-crafted의 필요성을 줄이고 potentially harmful tokenization schemes를 제거할 수 있다고 말합니다. 모델의 pretraining method는 Wikipedia English + C4 dataset 에 대해서 BERT와 동일한 MLM(Masked Language Modeling) 방식을 활용합니다.

![fig](/assets/images/perceiver-io/fig8.jpg)
<br>
위의 결과는 8 GLUE benchmark task에 대해서 UTF-8 bytes를 raw directly input data를 활용하여서, 각기 다른 Multitask 방법에 따른 실험 결과를 보여줍니다. single task의 경우는 a special token 을 함께 넣어주며 각각의 모델이 독립적으로 학습한 결과를 보여줍니다. shared input token의 경우는 a single token이 모든 task들에 대해서 사용됩니다. task specific input token의 경우는, 각 task마다 명시적으로 차이를 주는 방식입니다. 이러한 방법은 BERT에서 [CLS] token을 적용하는 것과 비슷한 방법이라고 생각할 수 있습니다. 한편, 본 모델이 제안하는 Multitask Query 에서는 이러한 [CLS] 꼴의 토큰이 필요가 없이 우수한 성능을 보이고 있으며, task의 수가 매우 많아질 때에는 더 매력적인 강점이 되게 됩니다.

![fig](/assets/images/perceiver-io/fig6.jpg)
<br>

## Reference
- <a href = "https://arxiv.org/abs/2107.14795"> Paper </a>

## The End 
- 다양한 IO를 다룰 수 있게 되었다는 점이 인상깊은 논문이었다. 
    - 정확한 쿼리로 정확한 information을 retrieval하기 위함이지만, 그럼에도 hand-desined한 query를 줘야 한다는 것이 결국은 조금 아직은 사람을 손을 타야 하는 것인가 하는 생각이 들었다. (더 나은 genral query를 줄 수 있는 후속 연구가 나올 거 같은 느낌..?)
- Starcraft II 의 AlphaStar의 agent unit selection policy를 결정짓는 pointer network을 대체하면서 한 실험에서는, '이런 다양한 데이터 모달리티를 포함함에도 결국은 이 조차도 general model이 되기 위한 하나의 module로서 쓰이는구나.' 하는 생각이 들었다. 다양한 데이터 모달리티를 다루는 것은 '지능'의 전부가 아니라 '하나의 충분조건'이다 라는 느낌을 받은 부분이었다. 더 어려운 문제를 풀거나, 더 깊은 추론이 필요한 문제, 환경이 급변하는 등의 문제에서는 역시 RL이 필요한 것인가 하고. RL 게을리 하지 말자.