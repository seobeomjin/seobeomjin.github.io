---
layout : post 
date : 2020-11-25
title : Codility Lessons Summary 
description : Codility Lessons 문제풀이를 요약합니다. 
publised : true
---
## Codility Lessons Summary 
<br>

#### Lesson 2 Array
- OddOccurrencesInArray / 배열의 요소 중 갯수가 짝수가 아닌 홀수 아이템을 찾는 문제 / easy 
```python 
    from collections import Counter 
    def solution(A):
        a = Counter(A)
        for k,v in a.items(): 
            if v%2 != 0 : 
                return k
        return 0
```
- Detected time complexity: O(N) or O(N*log(N))
    collection 을 하는데에 O(N) 이 들것이고, Counter를 돌면서 또 찾으니까, 최악의 경우에는 O(N/2) 경우가 또 들수도. <br>
    결국 for문 2번이 따로따로 돌면 O(2N) -> O(N)인가???????

#### Lesson 3 Time Complexity 
- FrogJmp / 개구리가 X에서 최소Y까지 가고 싶으며, D만큼 이동함. 최소 몇 회 이동해야 할까. 
```python
    # Detected time complexity: O(1)
    def solution(X, Y, D):
        yx = Y-X
        if not yx%D: # when 0 
            return yx//D 
        else : 
            return yx//D+1

    # REF) Efficient failed solution # Detected time complexity: O(Y-X) 나옴 -> 다시 
    def solution(X, Y, D):
        i = 0
        while X+D*i < Y :
            i += 1 
        return i
```

#### Lesson 4 Counting Elements
- ★ MaxCounters / N 사이에 값이 있으면 +1 , N+1이 값이면 max로 모든 counter값을 수정 / Medium (문제는 쉽지만 complexity 문제) <br>
```python
    # Detected time complexity: O(N + M) / 100% 
    def MaxCounters(N, A):
        # * max를 매번 계산하지 않는 것이 포인트 였을까?
        oper = [0]*N
        was_last_max = False
        max_val = 0
        for i in range(len(A)): 
            if A[i] <= N :
                oper[A[i]-1] += 1
                max_val = max(max_val, oper[A[i]-1])
                was_last_max = False # 왜 맥스를 여기서 비교할까/ -> 아래에서 뽑으려고 하면 연산 비용이 너무 비싸짐!!!
            elif not was_last_max :  # 일단 당연히 N+1이고, was_last_max 가 아닌 경우 
                oper = [max_val]*N
                was_last_max = True 
        return oper

    # Detected time complexity : O(N*M) / 66%
    def solution(N, A):
        """
        Array를 처음부터 돌아보며 진전시키는 방법 밖에 없을까?
        그 과정에서 연산을 어떻게 효율적으로 수행하는지 중요한걸까? 
        max로 바꿔주는 과정때문에 연산 순서를 바꿀 순 없어
        max가 나오기 전까지 다 더하고 max 로 바꾸지 말고 다 더해줘 
        """
        oper = [0 for _ in range(N)]
        max_val = 0
        for i in range(len(A)): 
            if A[i] > N+1 : continue 
            elif 1<= A[i] <= N : 
                if oper[A[i]-1] < max_val : 
                    oper[A[i]-1] = max_val + 1
                else :  
                    oper[A[i]-1] += 1 
            else : 
                max_val = max(oper) # oper가 얼마나 길줄 알고 그럴 때마다 자꾸 max를 매번 계산해?? 오점!!! 
        for j in range(N) : 
            if oper[j] < max_val : 
                oper[j] = max_val
        return oper
```
- 이번 문제는, max를 매번 뽑지 않고 한 번의 비교로 max를 계속 가지고 있는 것이 중요했던 것 같다. 

- MissingInteger / 
```python
    # returns the smallest positive integer
    #  N [1..100,000]
    #  each element of A [−1,000,000..1,000,000]

    # https://m.blog.naver.com/alwlren_00/221600041769 참고
    # sort 사용 100%
    def solution(A):
        A.sort()
        min = 1 
        for a in A : 
            if a == min : 
                min += 1
        return min

    # 100 % , Hash map 을 쓰는 방법, 근데 메모리를 너무 많이 먹게 되는 거 아닌가. 
    # Detected time complexity : O(N) or O(N * log(N))
    def solution(A):
        check = [0]*1000000 
        for a in A : 
            if a > 0 and check[a-1] == 0 : 
                check[a-1] +=1 
        for i in range(len(check)): 
            if check[i] == 0 : 
                return i+1


    # Detected time complexity : O(N) or O(N * log(N)) 
    # Correctness 100% / Performance 75% / 88 score 
    def solution(A): 
        sorted_arr = list(set(sorted(A)))
        tmp = [0]
        for i in range(len(sorted_arr)): 
            if sorted_arr[i] < 1 : 
                continue
            else :
                if sorted_arr[i] == tmp[-1]+1 : 
                    tmp.append(sorted_arr[i])
                else : 
                    return tmp[-1]+1
        if tmp[-1] == 0 : # 계속 값이 음수였던 경우.  
            return 1 
        else : return tmp[-1]+1 # 연속적으로 계속 들어있던 경우 
        """
        소팅을 해서 가장 작은 값을 뽑아야 할까 
        우선순서가 뒤죽박죽일거야 없는 것을 찾으려면 
        """
```


#### Lesson 5 Prefix Sums
- ★GenomicRangeQuery / 염기 타입 string의 어떤 ubstring에서 minimal impact factor 찾기/ Medium
```python
    def solution(S, P, Q): 
        """
        substring queries에서 S[P[i]:Q[i]+1] 에서 가장 작은 impact factor가 존재하는 값을 찾아야 하는 문제. 
        """

        # better method
        # Al, Cl, Gl = [0] * N, [0] * N, [0] * N
        # A, C, G = -1, -1, -1

        # for i, x in enumerate(S): # 인덱스 번호가 곧 갯수랑 같거든 
        #     if x == "A": A = i
        #     if x == "C": C = i
        #     if x == "G": G = i
        #     Al[i], Cl[i], Gl[i] = A, C, G 


        # my method 
        N, M = len(S), len(P)
        A, C, G = [-1]*N, [-1]*N, [-1]*N 
        for i in range(N): 
            if S[i] == 'A' : 
                if i != 0 :
                    A[i], C[i], G[i] = i, C[i-1], G[i-1]
                else : A[i], C[i], G[i] = i, -1, -1
            elif S[i] == 'C': 
                if i != 0 :
                    A[i], C[i], G[i] = A[i-1], i, G[i-1] 
                else : A[i], C[i], G[i] = -1, i, -1
            elif S[i] == 'G': 
                if i != 0 :
                    A[i], C[i], G[i] = A[i-1], C[i-1], i
                else : A[i], C[i], G[i] = -1, -1, i
            else : 
                if i != 0 :
                    A[i], C[i], G[i] = A[i-1], C[i-1], G[i-1]
                else : A[i], C[i], G[i] = -1, -1, -1

        # print(f'A {A} \nC {C}\nG {G}')
        ans = [0]*M
        for j in range(M): 
            ans[j] = 4
            if P[j] <= A[Q[j]] and A[Q[j]] <= Q[j] : 
                ans[j] = 1 
            elif P[j] <= C[Q[j]] and C[Q[j]] <= Q[j] : 
                ans[j] = 2 
            elif P[j] <= G[Q[j]] and G[Q[j]] <= Q[j] : 
                ans[j] = 3
        return ans
```
<br>
- prefix sum 개념을 적용해야 time complexity를 만족하며 값을 이룰 수 있음 <br>
    prefix summation 알고리즘은, 부분합(인덱스의 특정 부분)에 주로 사용되는 방법으로, 인덱스를 증가시킬 때마다 매 state의 sum을 구하고<br>
    특정 부분의 sum에서 다른 특정 부분의 sum까지 빼주는 방식으로 구성됨. <br>
    (위 문제에서는 인덱스가 진행되면서 가장 최근에 등장한 인덱스를 해당 타입의 status 인덱스에 넣어주는 식으로 tracking 함)<br>
- 여기에서는, 매 인덱스를 기준으로 가장 최근에 존재했던 위치의 인덱스를 넣어줌으로서 구현될 수 있음. <br>
- nucleotype_ID[] 가 P[i] ~ Q[i] 사이의 인덱스에서 nucleotype_ID[Q[i]] 가 존재하면 돼.   <br>

#### Sorting 
- Distinct / returns the number of distinct values in array A / Easy
```python
    #  100%
    def solution(A):
        # len(A) 0~100000
        return len(set(A))
```

- MaxProductOfThree / product of triplet 중에서 가장 큰 값을 뽑아라 / Easy
```python
    def solution(A):
        """
        순서상관없이 3개 지만 그렇게 하면 경우의 수 너무 많아서 안되고 
        값들을 소팅해서 max(뒤에서 3개 좌르륵, 앞에2개,뒤에하나) 해보자
        """
        # [3..100,000]len(A) / [-1,000..1,000] A 
        A.sort()
        return max((A[0]*A[1]*A[-1]), (A[-1]*A[-2]*A[-3]))
```

- NumberOfDiscIntersections / 배열의 인덱스가 의 중심 좌표, 값이 반지름일 때 각 원들이 겹치는 pair의 갯수를 구하라. / Medium
```python
    # https://github.com/Mickey0521/Codility-Python/blob/master/NumberOfDiscIntersections_v2.py
    # Detected time complexity: O(N*log(N)) or O(N) / 100%
    def solution(A): 
        N = len(A)
        lower, upper = [], []
        for i in range(N):
            lower.append(i-A[i])
            upper.append(i+A[i])
            
        sorted_lower = sorted(lower) # ( 가 낮은쪽 좌표부터 정렬 
        sorted_upper = sorted(upper) # ) 가 낮은 쪽 좌표부터 정렬 

        inter = 0 
        j = 0 
        for i in range(N):
            while (j<N and sorted_upper[i] >= sorted_lower[j]): 
            # 가장 낮은 좌표의 ) 보다, 같거나 작은 경우의 ( 가 존재하는 경우에 
            ###################이해가 안되는 부분 !!!!!!!! #####################
                inter += j # 앞에서 부터 그런 (인 j의 인덱스들을 더해주고 
                inter -= i # ( 인덱스를 빼준다. 
                j += 1 # 그리고 인덱스를 증가시킴. 
                # (i,j) : (0,0) / (i,j) : (0,1) / (i,j) : (0,2) / (i,j) : (0,3) 
                # / (i,j) : (1,4) / (i,j) : (3,5)
        return -1 if inter > 10000000 else inter

    # Detected time complexity : O(N**2)
    # score:  56 - Correctness 100% Performance 12%
    from math import factorial 
    def solution(A):
        N = len(A)
        if N < 1: 
            return 0
        N_combs = int((factorial(N))/(factorial(2)*factorial(N-2)))
        not_inter = 0 
        for i in range(N): 
            end_point = i + A[i]
            for j in range(i+1,N): 
                begin_point = j - A[j]
                if begin_point - end_point > 0 : 
                    not_inter += 1 
                else : continue 
        ans = N_combs - not_inter 
        if ans > 10000000 : return -1 
        else : return ans
```

#### Stack 
- Brackets /  / Easy
```python
    # 50 %  ( Correctness 100% Performance 20% )
    # Detected time complexity : O(3**N)
    def solution(S):
        # len(S) == [0..200,000]
        #  "(", "{", "[", "]", "}" and/or ")"
        s = list(S)
        stack = []
        while s : 
            item = s.pop(0)
            if not stack : 
                stack.append(item)
            else : 
                stack.append(item)
                if stack[-2] == '{' and stack[-1] =='}' or \
                stack[-2] == '(' and stack[-1] == ')' or \
                stack[-2] == '[' and stack[-1] == ']': 
                stack.pop(-1)
                stack.pop(-1)
        return 1 if not stack else 0
```
- 스택은 맞긴 한데, 각 페어쌍을 어떻게 비교해서 스택에서의 값과 비교할 것인지가 관건,, 