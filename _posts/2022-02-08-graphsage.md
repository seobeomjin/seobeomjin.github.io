---
layout: post
title: GraphSAGE paper review
subtitle: Inductive Representation Learning on Large Graphs 
categories: Paper review
tags: Graph unsupervised-learning
comments: True
published: True
---

## Summary 
<!-- - Problem Situation
- Poposed Work 
- Results -->
- 기존 상황 및 문제점 <br>
    large graph에서의 노드들의 low-dimensional embeddings 은 유용하나, 많은 방법론들이 embedding 을 학습 시 모든 node들이 존재해야 한다는 단점을 가지고 있습니다. 이러한 방법론은 transductive 하고 unseen nodes에 대해서 일반화가 되지 않는다는 단점을 가지고 있습니다. 

- 본 논문의 제안 <br>
    이에 본 논문에서는 GraphSAGE 라는 general inductive framework을 제안합니다. GraphSAGE 에서는 각 node에 대한 embedding을 학습하기보다는, embedding을 생성할 수 있는 function 을 각 feature embedding을 sampling & aggregating을 통해 학습시킵니다. 

- 실험 결과 <br>
    본 논문에서는 3 가지의 inductive node-classification 에 대해서 타 모델에 비해 outperformance를 달성합니다. 

## Main Contribution
- propose a general framework, called GraphSAGE (SAmple and aggreGatE)
    - leverage node features (e.g., text attributes, node profile information, node degrees) in order to learn an embedding function that generalizes to unseen nodes.
    -  learn the topological structure of each node’s neighborhood as well as the distribution of node features in the neighborhood.
    -  train a set of aggregator functions that learn to aggregate feature information from a node’s local neighborhood (Figure 1).

## Introduction

## Method
<figure>
	<img src="{{ '/assets/images/graphsage/Fig1.jpg' | prepend: site.baseurl }}" alt=""> 
</figure>

- Embedding generation (i.e., forward propagation) algorithm
    - Relation to the Weisfeiler-Lehman Isomorphism Test
- Learning the parameters of GraphSAGE
- Aggregator Architectur
    - Mean aggregator 
    - LSTM aggregat
    - Pooling aggregator
## Experiments

## Conclusion 

## Reference
- <a href="https://arxiv.org/abs/1706.02216"> Paper </a><br>

## 궁금했던 점 / 느낀 점