---
layout: post
title: GraphSAGE review
subtitle: Inductive Representation Learning on Large Graphs, 2017
categories: Paper-review
tags: graph unsupervised-learning large-graph
comments: True
published: True
---

## Summary 
<!-- - Problem Situation
- Poposed Work 
- Results -->
- 기존 상황 및 문제점 <br>
    large graph에서의 노드들의 low-dimensional embeddings 은 유용하나, 많은 방법론들이 embedding 을 학습 시 모든 node들이 존재해야 한다는 단점을 가지고 있다. 이러한 방법론은 transductive 하고 unseen nodes에 대해서 일반화가 되지 않는다는 단점을 가지고 있다. 

- 본 논문의 제안 <br>
    이에 본 논문에서는 GraphSAGE 라는 general inductive framework을 제안합니다. GraphSAGE 에서는 각 node에 대한 embedding을 학습하기보다는, embedding을 생성할 수 있는 function 을 각 feature embedding을 sampling & aggregating을 통해 학습시킨다. 

- 실험 결과 <br>
    본 논문에서는 3 가지의 inductive node classification task에 대해서 타 모델에 비해 outperformance를 달성한다. 
    
<!-- ## Main Contribution -->
<!-- - propose a general framework, called GraphSAGE (SAmple and aggreGatE)
- leverage node features (e.g., text attributes, node profile information, node degrees) in order to learn an embedding function that generalizes to unseen nodes.
-  learn the topological structure of each node’s neighborhood as well as the distribution of node features in the neighborhood.
-  train a set of aggregator functions that learn to aggregate feature information from a node’s local neighborhood (Figure 1). -->

<!-- ## Introduction -->
## Method
본 논문에서 제안하는 바의 key idea는 node의 local neighborhood로부터 feature information 을 어떻게 aggregate 할 수 있을 것인지에 관한 부분이다. 
따라서 embedding을 어떻게 generation 할 수 있는지, 그 다음 embedding을 어떻게 학습할 수 있는지에 대해 살펴보자.
<figure>
	<img src="{{ '/assets/images/graphsage/Fig1.jpg' | prepend: site.baseurl }}" alt=""> 
</figure>
위의 Figure1은 GraphSAGE가 sampling과 aggregate 을 통해 node embedding을 학습하는 과정을 시각화한 예시를 보여준다. 각 노드를 기준으로 fixed-size set of neighbors 에 대해서 uniform sampling 을 통해 주변의 이웃들을 sampling 해준다. sampling된 주변의 node embedding을 aggregate 해주고, 자기 자신의 node embedding과 정보를 concat하여 node embedding이 업데이트 된다. 자세한 내용은 아래의 과정에서 살펴보자.  

- Embedding generation (i.e., forward propagation) algorithm <br>
    <figure>
        <img src="{{ '/assets/images/graphsage/Fig2.jpg' | prepend: site.baseurl }}" alt=""> 
    </figure>
    - Embedding은 위의 Algorithm 과 같은 방식으로 생성된다. 주요한 line들에 대해 작동하는 방식을 살펴보면 아래와 같다.
        - line 4: k-1 layer에 있는 feature embedding h에서 neighborhood function 에 속해 있는 u node들에 대해 aggregate function 을 통해 neighborhood embedding $h_{N(v)}^k$를 얻어준다. <br>
        - line 5: 업데이트 대상이 되는 v node의 h embedding과 concat 을 해준 후, k layer의 weight matrix W를 곱해주어 새로운 embedding을 얻는다. 이후 nonlinear activation function 을 취해 $h_v^k$를 얻는다.<br>
        - line 7: hyperspere normalization을 취해 준다. 이렇게 normalization을 취해주면 NNS(Nearest Neighbor Search)에 유용하다고 하다.<br>
    - Relation to the Weisfeiler-Lehman Isomorphism Test
- Learning the parameters of GraphSAGE
- Aggregator Architecture
    - Mean aggregator 
    - LSTM aggregat
    - Pooling aggregator

## Experiments
![fig3](/assets/images/graphsage/Fig3.jpg) <br>

![fig4](/assets/images/graphsage/Fig4.jpg) <br>

<!-- ## Conclusion  -->

## Reference
- <a href="https://arxiv.org/abs/1706.02216"> Paper </a><br>
- <a href="https://www.youtube.com/watch?v=vinQCnizqDA&t=2s"> GraphSAGE Review Video </a><br>
## 느낀 점
- random permutation 을 수행한 LSTM aggregator function이 좋은 성능을 보인 것이 흥미로웠다. 
- MHSA(Multi Head Self Attention) aggregator function 을 활용하면 어떤 결과가 나올지 궁금하다. 
    - multi head를 이용하는 점, self-attention 이 inductive bias가 약한 점을 고려하면 더 다양한 관점의 feature를 내포할 수 있지 않을까? 
    
<!-- - 번외로, Trm과 GCN의 업데이트 방식이 유사하게 보이면서 차이점이 드러나는 게 흥미롭다. 
- Trm; MLP(MHSA(token embedding))
- GCN; MLP(A) -->
