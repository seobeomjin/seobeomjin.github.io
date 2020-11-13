---
layout : post 
date : 2020-11-13
title : Programmers 알고리즘 문제풀이 요약 
description : 알고리즘 문제풀이를 요약합니다. 
publised : true
---

## Programmers 코딩테스트 고득점 kit  
<br>

### Hash 
1. 마라톤 : 참가자,완주자 문자열 배열을 입력으로 주면 완주하지 못한 사람의 이름을 반환하는 문제<br>
```python
    import collections
    def solution(participant, completion):
        answer = collections.Counter(participant) - collections.Counter(completion)
        return list(answer.keys())[0]
```
2. 전화번호 목록 : 전화번호들이 담긴 배열이 주어지면 배열 내의 특정 번호가 또 다른 번호의 접두어로 겹치는지를 체크하는 문제 <br>
```python 
    def solution(phonebook):
        phonebook = sorted(phonebook)
        for p1, p2 in zip(phonebook, phonebook[1:]):
            if p2.startswith(p1): 
                return False 
    return True
```
3. 위장 : 스파이가 위장을 하며 매일 다른 옷을 입어야 하는 경우의 수 문제 <br>
```python
    items = []
    for cloth in clothes : 
        items.append(cloth[1])
    counter = collections.Counter(items) 
    # list에 있는 요소들이 각각 몇개씩 있는지를 딕형태로 돌려줌
    if len(counter.keys())!= 1 : 
        whole = 1
        for i in counter.values() : 
            whole *= (i+1)
    else : 
        sum_ = len(items)
        return sum_
    return whole-1
```
4. 베스트 앨범 : 장르별로 가장 많이 재생된 곡들을 상위 두곡씩 뽑아 베스트앨범 구성 Lv3 <br>
    ```python 
    def Q4_solution(genres, plays):
        answer = []
        d = {e:[] for e in set(genres)}
        print('d : ', d)
        for e in zip(genres, plays, range(len(plays))):
            print('e : ', e)
            d[e[0]].append([e[1] , e[2]])  # e[0]->genres 이고, 이미 아까 리스트로 만들어 두었으니 append가 되는구나
        print('after d : ', d) 
        # {'pop': [[600, 1], [2500, 4]], 'classic': [[500, 0], [150, 2], [800, 3]]}
        # 딕셔너리 형태로 각 고유번호와 재생 횟수를 넣었음
        # genreSort = sorted(list(d.keys()), key= lambda x: sum( map(lambda y: y[0],d[x])), reverse = True)
        genreSort =sorted(list(d.keys()), key= lambda x: sum([t[0] for t in d[x]]), reverse = True) 
        # t[0] 600, 2500 같은 재생 횟수 # map(function , list) -> 리스트에 있는 값들을 하나씩 꺼내서 함수를 적용 # d[x] 여기서 x는 각 dict의 key
        # 오름차순이기 때문에 reverse=True로 해서 내림차순으로. 
        # genre sort :  ['pop', 'classic']
        for g in genreSort:
            temp = [e[1] for e in sorted(d[g],key= lambda x: (x[0], -x[1]), reverse = True)] # 해당 장르의 리스트 내에서 정령 안에서 e[1]을 꺼내는 것 
            # 600 -1
            # 2500 -4
            print('temp : ',temp)
            answer += temp[:min(len(temp),2)]
        return answer

    # reduce # 리스트의 값들을 누적적으로 실행 
    from functools import reduce 
    reduce(lambda x, y: x + y, [0, 1, 2, 3, 4])
    >>> 10

    # filter # 리스트에서 참인 값들을 반환
    >>> list(filter(lambda x: x < 5, range(10))) # 파이썬 2 및 파이썬 3
    >>> [0, 1, 2, 3, 4]
    # 참의 값만 통과시켜 내줌
    ```



### Exhaustive Search
1. 모의고사 : 수포자 학생 세명이서 어떤 규칙을 통해 문제를 찍었고, 문제의 답이 배열로 주어질 때 가장 많이 맞춘 학생을 return, 동점일 시 오름차순으로 배열<br>
```python 
    def solution(answers):
    answer =[]
    no1 = [1,2,3,4,5] # 5로 계속 반복 / 0,1,2,3,4,  5,6,7,8,9, 10,11,12,13,14, 
    no2 = [2,1,2,3,2,4,2,5] # 8로 
    no3 = [3,3,1,1,2,2,4,4,5,5] # 10으로 
    count = [[1,0], [2,0], [3,0]]
    for idx in range(len(answers)): 
        if answers[idx] == no1[idx%5] : 
            count[0][-1] +=1 
        if answers[idx] == no2[idx%8]:
            count[1][-1] += 1 
        if answers[idx] == no3[idx%10]: 
            count[2][-1] += 1
    # 방법 1         
    sorted_count = sorted(count, key=lambda x : x[:][-1], reverse=True)
    # print("sorted : ",  sorted_count)
    answer.append(sorted_count.pop(0))
    while sorted_count : 
        if answer[-1][-1] == sorted_count[0][-1]:
            answer.append(sorted_count.pop(0))
        else : break 
    ans = [ answer[i][0] for i in range(len(answer))]

    # 방법 2 :만약 count = [0,0,0] 으로 잡은 경우라면 sort도 할 필요 없고 아래와 같이 짜면 됨 
    # for idx, s in enumerate(count): 
    #     if s == max(count) :
    #         ans.append(idx+1)
    return ans    
``` 
<!-- ### DFS /BFS  -->
### Sort
1. K 번째 수 : 배열이 주어지고 배열에서 특정i,j 인덱스를 sort 했을 때 k 번째 인덱스 찾기) Lv1 <br>
    ```python 
    def solution(array, commands):
        answer = []
        for command in commands :
            answer.append(oper(array, command))
        return answer

    def oper(arr, command):
        cropped = []
        cropped = arr[command[0]-1 : command[1]] # 2번째에서 5번째 니까 인덱스 1에서 
        sorted_cropped = sorted(cropped)
        return  sorted_cropped[command[2]-1]
    ```
2. 가장 큰 수 : 수들이 차례대로 들어있는 배열이 들어있고 그걸 이어 붙여 만들 수 있는 가장 큰 수 찾기 Lv2 <br>
    ```python
    def solution(numbers):
        numbers_str = list(map(str,numbers))
        sorted_numbers_str = sorted(numbers_str, key= lambda x : x*5 ,reverse=True)
        return str(int(''.join(sorted_numbers_str)))
    ```
    - 첫 글자의 크기(ASCII) 순서대로(오름차순) 2) 글자의 크기가 같다면 그 다음 길이를 체크.<br>

3. H-Index : 주어진 배열에서 h보다 큰 값이 h개 이상 존재하는 h의 최댓값 구하기Lv2 <br>
    ```python
    def solution(citations):
        answer = 0
        sorted_citations = sorted(citations)
        totals = len(citations)
        H_index = []
        for h in range(totals+1): 
            for j in range(totals): 
                if sorted_citations[j] < h : 
                    pass 
                else : 
                    if len(sorted_citations[j:]) >= h : 
                        H_index.append(h)
        return max(H_index)
    ```

### Stack / Que 
1. 주식가격 : 초 단위로 기록된 주식가격에서 가격이 이후 떨어지지 않은지가 몇초가 되는지를 return 하도록 함수를 구성하라. Lv2 <br>
    ```python 
    def Q1_solution(prices): 
        answer = [0] * len(prices)
        for i in range(len(prices)): # 0 - 4
            for j in range(i+1,len(prices)): # range(1,5) 1,2,3,4  
                if prices[i] <= prices[j] :
                    answer[i] += 1 
                else : 
                    answer[i] += 1 
                    break 
            if i == len(prices)-1 : 
                answer[-1] = 0
                break 
        return answer
    # print(Q1_solution([1, 2, 3, 2, 3]))
    ```
2. 기능개발 : 앞의 개발이 끝나야 뒤의 개발도 release될 수 있음. Lv2 <br>
    ```python 
    def Q2_solution(progresses, speeds):
        answer = []
        time , count = 0 ,0
        while len(progresses) > 0 : 
            if progresses[0] + time*speeds[0] >= 100 : 
                progresses.pop(0)
                speeds.pop(0)
                count += 1
            else : 
                if count > 0 : 
                    answer.append(count)
                    count = 0 
                time += 1
        answer.append(count) 
        return answer 
    # print(Q2_solution([93, 30, 55],[1, 30, 5]))
    ```
- 순차적으로 진행이니까 들어오는대로 처리되게 만들어야 함. 
- 맨 앞의 것부터 시간 순으로 처리. <br>

3. 다리를 지나는 트럭 : 트럭들이 순서대로 특정 무게를 견딜 수 있는 다리 위를 지나갈 때, 모든 트럭이 다리 위를 건너는 데에 걸리는 최소시간 return Lv2 <br>
    ```python 
    def Q3_solution(bridge_length, weight, truck_weights):
        # 사실 지나간다가 아니고 그 특정 시간동안만 있으면 
        time = 0 
        bridge = [0] * bridge_length 
        while bridge : 
            # print(bridge)
            time += 1 
            bridge.pop(0)
            if truck_weights : 
                if sum(bridge) + truck_weights[0] <= weight : 
                    bridge.append(truck_weights.pop(0))
                else : 
                    bridge.append(0)
            # print(bridge)
        return time
    # print(Q3_solution(2,10,[7,4,5,6]))
    ```
- 이 풀이의 핵심은, 1초가 지날 때마다 앞에서 0을 하나씩 빼고, 뒤에서 아이템을 하나씩 더해주는데, 다리의 무게에 제약을 주어서 무게를 버틸 수 있으면 + next truck 이고 아니면 그냥 0(index) 추가임<br>

4. 프린터 : 중요도가 높은 문서를 먼저 인쇄하도록 구성. 
    ```python 
    def solution (p, l) :  # priorities , location 
        order = 0
        queue = [(i,p) for i, p in enumerate(p)]
        while queue : 
            cur = queue.pop(0)
            if any(cur[1] < q[1] for q in queue): 
                queue.append(cur)
            else : 
                order += 1 
                if l == cur[0]: 
                    return order
    # print(Q4_solution([2, 1, 3, 2], 2))
    # print(Q4_solution([1, 1, 9, 1, 1, 1],0))
    ```
- enumerate를 이용해 우선순위와 인덱스를 함께 잡고, any문을 통해 현재의 우선순위가 가장 높으면 order += 1 해주면서 loc비교 
- I thought) 인덱스가 필요한 경우에는 인덱스(고유번호)를 어떻게 함께 가지고 다닐지 고민해야 함. (enumerate 라던가, dict 이라던가 ) 




<!-- ### Heap  -->

<!-- ### DP  -->
<!-- ### Greedy  -->
<!-- ### Binary Search  -->
<!-- ### Graph  -->



- 프로그래머스 고득점 kit
    - Hash 4/4 (DONE)
    - 완전탐색 1/3
    - 깊이/너비 우선 탐색 
    - 정렬 3/3 (DONE)

    - Stack/Que 4/4 (DONE)
    - 힙 
    
    - DP
    - 탐욕법 
    - 이분탐색
    - 그래프