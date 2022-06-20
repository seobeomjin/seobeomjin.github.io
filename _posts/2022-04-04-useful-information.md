---
layout: post
title: ML/DL knowledges
subtitle: Collecting useful information about DL/ML
categories: Study
tags: modeling
comments: True
published: True
---

<!-- #### Sigmoid VS Softmax  -->
- <b> Sigmoid VS Softmax </b>
    - Sigmoid 
        - probabilities produced by a Sigmoid are independent. (변수들이 독립적으로 계산됨) <br>
        - they are *not* constrained to sum to one. The reason for this is because the Sigmoid looks at each raw output value separately. <br>
        - Used for Binary Classification in the Logistic Regression model <br>
        - **Sigmoid** is equivalent to a 2 element **Softmax**, where the second element is assumed to be zero. Therefore, **sigmoid** is mostly used for **binary classification**.

    - Softmax 
        - the outputs are interrelated. The Softmax probabilities will always sum to one by design: 0.04 + 0.21 + 0.05 + 0.70 = 1.00. In this case, if we want to increase the likelihood of one class, the other has to decrease by an equal amount. <br>
        - Used for Multi-classification in the Logistics Regression model <br>
        - **softmax** is specially designed for **multi-class** and **multi-label** classification tasks. <br>

- <b> Receptive field </b><br>
    CNN에서 kernel size를 통해 볼 수 있는 window 의 크기이다. receptive field 가 크면 더 넓은 영역을 cover하여 다음 feature를 뽑을 수 있고, 그 영역이 작으면 더 local 한 정보에 집중하게 된다. <br>

- <b> Inductive bias </b><br>

- <b> Fourier Features </b><br>

- <b> Over-smoothing (in graph) </b><br>
    GNN에서 Over-smoothing이란 Graph 층이 깊어지면서 Graph embedding이 general 한 범위에서 feature 가 지나치게 일반화되는 것을 말한다. <br>

- <b> Maksed Auto Encoder </b><br>
    최근(2022년 6월 기준) 많이 사용되고 있는 self-supervised learning 방법론. <br>
    original input 의 일부를 masking 처리 없이 입력으로 줘서 encoder 를 지난 latent vector를 뽑는다. <br>
    latent vector 에 masking 처리를 하여 decoder에 입력을 주고, target image 를 예측하도록 만든다. <br>

<!-- #### Receptive field 
#### Inductive bias
#### Fourier Features 
#### Over-smoothing (in graph) -->

#### Reference 
- https://medium.com/deep-learning-with-keras/which-activation-loss-functions-part-a-e16f5ad6d82a#:~:text=The%20practical%20reason%20is%20that,mostly%20used%20for%20binary%20classification.
- https://www.dacon.io/forum/405840

