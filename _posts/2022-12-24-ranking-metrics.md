---
layout: post
title: ranking metric (MRR, MAP, NDCG) 공부
subtitle: Information Retrieval Evaluation metric 에 대해 공부합니다. 
categories: Study
tags: ranking metric information-retrieval
comments: True
published: True
---

### MRR (Mean Reciprocal Rank)

- Reciprocal Rank 의 평균 값을 나타낸다. 
    - Reciprocal Rank 란, <br>
        model 이 positive 라고 prediction 한 item이 몇 번 째에 나오는지를 나타낸다. <br>
        예를 들어, 3번째에 등장하면 1/3 값, 첫 번째에 등장하면 1/1 값이다. <br>
        (앞에 등장할수록 더 큰 값을 갖는다.) <br>
- 장점 <br>
    가장 앞에 positive item이 언제 등장하는지에 초점을 맞춘다면, 효과적인 metric
- 단점 <br>
    뒤에 얼마나 많이 positive item이 나오는지 등은 고려하지 않는다. <br>
    또한 뒤에 얼마나 많은 negative item 이 나오는지도 고려하지 않는다. <br>
    (그저 최초의 positive item이 언제 나오는지만 고려함)<br>

### MAP (Mean Average Precision)

- Average Precision의 평균값이다. 
    - 여기서 Average Precision 이란, <br>
        positive item이 등장할 때마다의 sublist에 대해서 average precision 값을 구한다. <br>
        예를 들어, O X O O X 의 경우, ((1/1) + (2/3) + (3/4)) / 3 = 0.8 이다. <br>
    - 이 값을 모든 user 에 대해 평균을 낸 값이 Mean Average Precision 이다. 
- 장점 <br>
    맨 앞의 값 뿐만 아니라, 뒤에 얼마나 빈번하게 positive item이 나오는지를 관찰할 수 있다. <br>
    더 상위에 올 수록 값을 크케 받을 수 있게 한다. <br>
- 단점 <br>
    pos/neg 를 구분할 때, 1~5 점 사이의 점수를 기반으로 mapping이 되어있으면, 이를 pos/neg 구분이 불명확하다(??) (binary면 좀 더 명확할텐데, 이는 그렇지 못한 경우를 말하나 보다.)

### NDCG (Normalized Discounted Cumulative Gain)

- ideal ranking 이 (model predicted) real ranking 사이의 차이가 얼마나 나는지를 보여준다. 
- ideal ranking ; highly related contents 가 앞 쪽에 우선 배치되는 이상적인 retrieval case 이다. 
- ideal ranking과 real ranking 각각 따로따로 cumulative gain 을 summation 해서 구한다. ideal ranking 의 경우는 모든 real ranking에 비해서 값이 크거나 같다. 
-  0 <= NDCG <=1
   NDCG = sum(cumulative gain of real ranking) / sum(cumulative gain of ideal ranking)

### Reference
- https://lamttic.github.io/2020/03/20/01.html