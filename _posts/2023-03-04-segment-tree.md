---
layout: post
title: \[알고리즘] Segment Tree (Python)
subtitle: segment tree 
categories: Study  # [Paper-review, Study] 
tags: algorithm segment-tree
comments: True
published: True
---

# Segment Tree 
- 언제 쓰는가 <br>
    - 특정 구간에 속한 연산 (합, 최솟값, 최댓값 등) 을 할 때, 선형탐색 대비 더욱 빠르게 가능. <br>
    - 누적합과의 차이 <br>
        - 누적합은 합만을 다룸 <br>
        - 어떤 값이 업데이트 될 경우, O(N) 으로 업데이트 해야 함 <br>
        - segment tree는 O(logN) 으로 업데이트 가능 <br>

# Reference
- https://yiyj1030.tistory.com/491#:~:text=%EC%84%B8%EA%B7%B8%EB%A8%BC%ED%8A%B8%20%ED%8A%B8%EB%A6%AC%20%EA%B5%AC%ED%98%84,%EC%9D%B8%EB%8D%B1%EC%8A%A4%EB%8A%94%201%EB%B2%88%EC%9D%B4%EB%8B%A4.
- https://velog.io/@corone_hi/%EA%B5%AC%EA%B0%84-%ED%8A%B8%EB%A6%AC-Segment-Tree-Python