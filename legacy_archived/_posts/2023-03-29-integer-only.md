---
published: false
layout: post
title: 2018 CVPR, Quantization and Training of Neural Networks for Efficient Integer-Arithmetic-Only Inference 
subtitle: Efficient Integer-Arithmetic-Only Inference 논문 리뷰 내용의 후기를 적어봅니다.
categories: Paper-review  
tags: quantization inference data-type
comments: True
---


## Introduction 
- 논문의 제안
    - weight 와 activation 모두 int-quantization해서 inference time 에 integer 연산만 활용하겠다. 
    (opinion. 23년 기준의 다른 PTQ 알고리즘들에서의 integer quant의 기법들도 이런 작용을 거치는 것인가?💥)
- Activation 이란?
    Inference time에 input에 따라 값이 변하는 variable   
- Low Precicion benefits 
    적은 메모리 사용 / 빠른 컴퓨테이션 속도 / 전력 소비 감소 / AI accelerators 활용 가능 

## Quantized Inference
- Quantization Scheme 
    - 실수 r을 어떤 정수 q에 mapping 시킬 것인가? 를 고민하는 문제 
    - r = S(q-Z)     
    - S 
        = scaling factor 
        = (rmax-rmin) / 2^N such that N is number of quantization bit
    - Z = -round(rmin/S)
    - S,Z는 실수 범위에 따라 정해지는 quantization parameter 
    - 각 layer의 array에 존재하는 실수 R과 정수 Q 사이의 S,Z 값은 공유  

- Matrix Multiplication 
    - Example 
        r3 = r1 * r2 matmul 연산이 있음. 
        S3(q3-Z3) = S1(q1-Z1) * S2(q2-Z2) 일 때, q1,q2를 알면 q3을 구할 수 있을까? 

- Typical Fused Layer 


## Training with Simulated Quantization 
- motivation 
    - common approach 
        - 
        -
    - common approach 는 small model 에서 적용되지 않는다 
        - 
        -
    - 따라서 quantization effect 를 training time의 forward pass 에 적용해 보고자 한다.

## Experiments

    