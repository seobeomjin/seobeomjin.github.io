---
layout: post
title: ML/DL knowleges
subtitle: Collecting useful information about DL/ML
categories: Study
tags: modeling
comments: True
published: True
---

#### Sigmoid VS Softmax 
- Sigmoid 
    - probabilities produced by a Sigmoid are independent. (변수들이 독립적으로 계산됨) <br>
    - they are *not* constrained to sum to one. The reason for this is because the Sigmoid looks at each raw output value separately. <br>
    - Used for Binary Classification in the Logistic Regression model <br>
    - **Sigmoid** is equivalent to a 2 element **Softmax**, where the second element is assumed to be zero. Therefore, **sigmoid** is mostly used for **binary classification**.

- Softmax 
    - the outputs are interrelated. The Softmax probabilities will always sum to one by design: 0.04 + 0.21 + 0.05 + 0.70 = 1.00. In this case, if we want to increase the likelihood of one class, the other has to decrease by an equal amount. <br>
    - Used for Multi-classification in the Logistics Regression model <br>
    - **softmax** is specially designed for **multi-class** and **multi-label** classification tasks. <br>

#### Receptive field 

#### Inductive bias

#### Fourier Features 

#### Over-smoothing (in graph)

#### Reference 
- https://medium.com/deep-learning-with-keras/which-activation-loss-functions-part-a-e16f5ad6d82a#:~:text=The%20practical%20reason%20is%20that,mostly%20used%20for%20binary%20classification.
