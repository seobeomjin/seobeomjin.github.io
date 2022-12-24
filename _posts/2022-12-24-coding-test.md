---
layout: post
title: 내가 보려고 정리하는 코딩 테스트 테크닉
subtitle: 코딩 테스트 테크닉에 대해 정리합니다.
categories: Study
tags: c++ coding-test
comments: True
published: True
---

- C++ 기준 1초 수행시간은 대략 1억의 연산이 든다. 
- 함수 수행횟수, 배열 사이즈 등을 유심히 보고 → variable 사이즈 잡기

- lower_boud, upper_bound
    - set에서 뭔가 낀 data(날짜 등)를 찾아낼 때 유용하다. 

- 계속 증가하는 변수가 있는데, 고정된 사이즈를 사용해야할 경우, two pointer - st, end pointer
- 양음 인덱스를 활용한 flag (400회 수행하거나 그런 경우?)

- 적절한 itemization이 가능하고, 각각의 요소에 접근해서 처리를 해야 하는 경우는 그냥 array로 접근해서 처리하기도 함.
- data가 앞으로도 push 되고, 뒤로도 push 되어야 한다면, deque container 활용하기 
- moduler로 나누는 경우는, hash로 가져갈 수 있다. 