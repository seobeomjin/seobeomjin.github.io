---
layout: post
title: Deep Spectral Methods
subtitle: A Surprisingly Strong Baseline for Unsupervised Semantic Segmentation and Localization, 2022, CVPR Oral
categories: Paper-review
tags: self-supervised-learning segmentation unsupervised-learning computer-vision localization eigendecomposition
comments: True
published: True
---

### Abstract

- Unsupervised localization and segmentation are long-standing computer vision challenges
    - that involve decomposing an image into semantically meaningful segments without any labeled data
- interesting in an unsupervised setting
    - due to the difficulty and cost of obtaining dense image annotations,
    - but existing unsupervised approaches struggle with complex scenes containing multiple objects.
- we
    - take inspiration from **traditional spectral segmentation methods** by **`reframing image decomposition as a graph partitioning problem`**.
    - **examine the eigenvectors of the Laplacian of a feature affinity matrix from self-supervised networks.**
    - **find that these eigenvectors already decompose an image into meaningful segments**, and can **be readily used to localize objects** in a scene
    - Furthermore, **by clustering the features associated with these segments across a dataset,** we can obtain well-delineated, nameable regions, i.e. semantic segmentations.
    - our simple spectral method outperforms the state-of-the-art in unsupervised localization and segmentation by a significant margin
    - this method can be readily used for a variety of complex image editing tasks, such as background removal and compositing.

<!-- - 한글 요약 
    - 전통적인 spectral segmentation 방법론에서 영감을 받아, unsupervised image decompistion 문제를 graph partitioning problem 관점에서 해결함. <br>
    - 순서 
        1. SSL 모델을 기반으로 image patch 에 대한 dense feature 추출 
        2. weighted -->


### Method
![method](/assets/images/deep-spectral-methods/method.png)<br>

      
