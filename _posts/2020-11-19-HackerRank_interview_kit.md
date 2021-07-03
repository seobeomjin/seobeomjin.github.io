--- 
layout : post
date : 2020-11-19
title : HackerRank Algorithm Kit Summary
description : HackerRank 알고리즘 문제풀이를 요약합니다. 
published : false
---

## HackerRank Interview  Preparation Kit 
<br>

<!-- ### Warm-up Challenges 
1. Sales by Match : make them as a pair and then count them how many pairs there are / easy / 7min  
```python 
    import collections 
    # Complete the sockMerchant function below.
    def sockMerchant(n, ar):
        counter_dict = dict(collections.Counter(ar)) #{10: 4, 20: 3, 30: 1, 50: 1}
        ans = 0
        for k,v in counter_dict.items(): 
            ans += v//2
        return ans
```
2. Counting Valleys : count how many valleys when a hiker take their hikes . / easy / 20min 
```python 
    def countingValleys(steps, path):
    # Write your code here
    # 0에서 +1로 가면 mountain이고 , -1로 가면 valley임 
    # 0 다음 -1이 몇개인지 체크 
    status = 0
    valley_count = 0 
    for p in path : 
        if p == 'U': status += 1
        else :
            if status == 0 : valley_count +=1 
            status -= 1
    return valley_count
```
3. Jumpinh on the Clouds : count how many jumps Emma should , for arriving there. / easy / 13min 집중! 
```python
    def jumpingOnClouds(c):
    # greedy? 
    # 매 state마다 최적의 선택을 하도록? 
    # 두칸씩 뛰어라 1이 아니면 
    count = 0 
    state = 0 
    while state < (len(c)-1) : 
        if state+2<=len(c)-1 and c[state+2] != 1 : 
            state += 2
            count +=1  
        else: 
            state +=1
            count +=1   
    return count
```
4. Repeated String : count how many character 'a' would be repeated in a repeated string / easy / 
```python 
    def repeatedString(s, n):
        # divide n strings by len(s)
        s_len = len(s)
        a_inS =0 # not index, just order from 1st ,2nd,,, 
        for char in s : 
            if char  == 'a' : a_inS +=1 
        total_count = a_inS*(n//s_len) 
        for i in range(n%s_len) : 
            if s[i] == 'a': total_count +=1 
        return total_count 
``` -->

### Arrays 
1. 2D Array - DS : access to each index of 2D array and then get biggest sum value / easy / 14min 
```python 
    # Complete the hourglassSum function below.
    def hourglassSum(arr):
        glass_sum_list = []
        for row in range(len(arr)-2):
            for col in range(len(arr)-2): 
                glass_sum_list.append(calc_glassSum(arr,row,col))
        return max(glass_sum_list) 
        
    def calc_glassSum(arr, row, col): 
        glass_sum = 0 
        for i in range(3): 
            for j in range(3):
                glass_sum += arr[row+i][col+j]
        glass_sum -= arr[row+1][col+0]
        glass_sum -= arr[row+1][col+2]
        return glass_sum
```

2. Arrays: Left Rotation / easy
```python 
    def rotLeft(a, d):
    # my plan 
    # I am gonna use que for each time and then put that item to the end  
    # a = [i+1 for i in range(len(a))]
    while d : 
        a.append(a.pop(0))
        d -=1   
    return a

    if __name__ == '__main__':
        ...
        fptr.write(' '.join(map(str,result))) # space separated string
        ... 
```

3. ★New Year Chaos / 한 사람당 2회씩 뇌물을 주어 줄을 선 것을 바꿀 수 있음. 해당 줄에서 총 뇌물을 교환한 횟수는? / Medium / But It is so ,, complicated for me ★
```python 
    def minimumBribes(q):
        # bubble sort ?
        arr = [ [idx, item-1] for idx,item in enumerate(q) ]
        # Too chaotic case
        # 뇌물을 준 경우는, 실제값이 인덱스보다 2이상 더 큰 경우. 2보다 크면 2회이상 주었다는 뜻. 
        for i in arr : 
            if i[1]-i[0] > 2 : 
                print("Too chaotic")
                return
                # return "Too chaotic"
        # calculate count case 
        count = 0 
        st = 0
        while st < len(arr) -1 : 
            if arr[st][0] == arr[st][1] : 
                st +=1 
                continue 
            for i in range(st,len(arr)): 
                if i < len(arr)-1 and arr[i][1] > arr[i+1][1] : 
                    bigger = arr[i][1]
                    arr[i][1] = arr[i+1][1]
                    arr[i+1][1] = bigger 
                    count +=1 
        print(count)
        return

    ###### 다른 풀이 
    def minimumBribes(Q):
    # initialize the number of moves
    moves = 0 
    # decrease Q by 1 to make index-matching more intuitive so that our values go from 0 to N-1, just like our indices.  
    # (Not necessary but makes it easier to understand.)
    Q = [P-1 for P in Q]
    # Loop through each person (P) in the queue (Q)
    for i,P in enumerate(Q):
        # i is the current position of P, while P is the original position of P.
        # First check if any P is more than two ahead of its original position
        if P - i > 2:
            print("Too chaotic")
            return
        # P의 원래 위치보다 앞서있는 것이 무엇인지 확인하라,,, 
        for j in range(max(P-1,0),i):
            if Q[j] > P:
                moves += 1
    print(moves)
    # From here on out, we don't care if P has moved forwards, it is better to count how many times
    # P has RECEIVED a bribe, by looking at who is ahead of P.  P's original position is the value of P.
    # Anyone who bribed P cannot get to higher than one position in front if P's original position,
    # so we need to look from one position in front of P's original position to one in front of P's
    # current position, and see how many of those positions in Q contain a number large than P.
    # In other words we will look from P-1 to i-1, which in Python is range(P-1,i-1+1), or simply
    # range(P-1,i).  To make sure we don't try an index less than zero, replace P-1 with max(P-1,0)
```
- 어려웠던 점 <br>
    1) 일단 문제 해석이 너무 난해했음. <br>
    2) sort를 할 생각을 왜 못했는지. 반성. Array라는 것에 갖혀 너무 쉽게 생각했음. <br>
       >>> 문제의 틀에 갖히지 말 것.<br>
    3) 직접 sort를 할 필요없이 swap된 횟수만을 계산하면 complexity를 낮출 수 있음. <br>
       >>> 하지만 코드 이해를 잘 못했다. 이거 할 것. <br>
<br>

4. ★Minimum Swaps 2 / 임의의 두 원소를 최소 swap하여 오름차순으로 만드는 것 / Medium <br>
```python
    # 첫 번쨰 풀이 : 선택 정렬로 풀었는데, Time limit exceeded 문구가 떴음. (12min) 
    ### Time limit exceeded ..!  12min 
# selection sort
def minimumSwaps(arr):
    idx =0 
    tmp = 0
    cnt = 0
    while idx < len(arr)-1 : 
        if arr[idx] == idx+1 : 
            idx += 1 
            continue 
        for i in range(idx,len(arr)): 
            if arr[i] == idx+1 : 
                tmp = arr[idx]
                arr[idx] = arr[i]
                arr[i] = tmp 
                cnt +=1    
                idx +=1 
                continue
    return cnt
```
- 포인트는 선택한 아이템을 원래 있어야 하는 자리로 보내면서 소팅하는 것임 <br><br>
- 두 번째 풀이 <a href = "https://somjang.tistory.com/entry/HackerRank-Array-Minimum-Swaps-2-Python"> 참고 </a> <br>
- 포인트는, 해당 인덱스가 있어야 하는 자리에 위치해 있지 않을 때, 그 값을 바꿔야 하는 자리에 가져다 놓음으로써 해결할 수 있었음. <br>
```python 
    def minimumSwaps(arr):
        tmp = 0
        cnt = 0
        for i in range(len(arr)): 
            while (arr[i]!= i+1): 
                tmp = arr[i] 
                arr[i] = arr[tmp-1]
                arr[tmp-1] = tmp
                cnt +=1 
        return cnt
# 버블 , 선택, 삽입 / 퀵 , 힙, 병합, 셀
# 도 딱히 아닌,,(?)
```

### Dict and Hash 
1. Hash Table : Ransom Note / easy / 20min <br>
```python 
    import collections 
    def checkMagazine(magazine, note):
        m = collections.Counter(magazine)
        n = collections.Counter(note)
        result = n - m 
        if result : 
            print("No")
        else : print("Yes")
```

2. Two Strings / easy / 9min 
```python 
    def twoStrings(s1, s2):
    s1_ = set([i for i in s1]) 
    s2_ = set([i for i in s2])
    if set(s1_).intersection(set(s2_)): 
        return "YES"
    else : return "NO"
```

3. ★Sherlock and Anagrams / 스트링에서 서브스트링의 "순차적인" 구성을 통해서 만들 수 있는 anagram(재배열된 서브스트링)의 갯수/ Medium
```python
    import collections
    def sherlockAndAnagrams(s):
        count = 0 
        for N in range(len(s)-1): # N을 갯수로 사용 # N+1개씩 체크 
            idx = 0 
            while idx <= (len(s)-1)-(N) :     #0개, 1개, 2개, ... n-1개
                item = s[idx:(N+1)+idx]
                i_ = collections.Counter(item) ############# 이걸 안에서 계산할 필요가 없으니까
                for j in range(idx+1,(len(s)-1)-(N)+1): # 마지막에서 N개 앞, 즉 마지막 N개까지 접근 가능한 곳까지.
                    f_ = collections.Counter(s[j:j+(N+1)])
                    if f_ == i_ : # f_ - i_ 가 아니라 바로 비교 
                        count +=1 
                    else : continue
                idx+=1
        return count 
    ############ 다른 솔루션 
    from collections import Counter
    def count_anagrams(string):
        buckets = {}
        for i in range(len(string)):
            for j in range(1, len(string) - i + 1):
                key = frozenset(Counter(string[i:i+j]).items()) # O(N) time key extract
                buckets[key] = buckets.get(key, 0) + 1
        count = 0
        for key in buckets:
            count += buckets[key] * (buckets[key]-1) // 2
        return count
```
- 왜 아이디어가 잘 안 떠오를까... 효율적인... 

4. ★★★Count Triplets / a,ar,arr 의 값이 순차적으로 배치된 것의 갯수를 찾는 문제 / Medium 
```python 
    # 1. Terminated due to timeout :(    7/13 correct 
    # for 문을 이렇게 돌려서는 못 찾는다.
    def countTriplets(arr, r):
    count = 0 
    case_dict = {}
    for idx, item in enumerate(arr): 
        case_dict[item] = case_dict.get(item,[])
        case_dict[item].append(idx)
    for k in case_dict.keys(): 
        if k*r and k*r*r in case_dict.keys(): 
            for i in case_dict[k]: 
                for j in case_dict[k*r]:   
                    if i < j : 
                        for p in case_dict[k*r*r]: 
                            if j<p : 
                                count += 1 
    return count 
    ####################################################### 
    # 2. another solution 
    def countTriplets(arr, r):
    count_dict = {}
    pair_dict = {}
    count = 0 
    for i in arr[::-1]:  # 인덱스도 따져야 하기 때문에 뒤에서부터 
        if i*r in pair_dict : # i 기준에서, i*r 이 pair_dict에 들어있다는 소리는 i*r ,  i*r*r 의 pair 를 말함 
            count += pair_dict[i*r]
        if i*r in count_dict : # i 기준에서  i*r이 이미 있으면 pair로 만들수 있으며 이미 뒤에 있는 인덱스를 의미하기 때문에 인덱스를 따질 필요조차 없음!!!!! (말이되는 아이디어인가!!)
            pair_dict[i] = pair_dict.get(i,0) + count_dict[i*r]
        
        count_dict[i] = count_dict.get(i,0) +1 # 매번 아이템을 카운트해주며 추가  
    return count
```
- a,ar,arr이 index또한 순서대로 구성되어 있어야 했기 때문에 뒤에서 부터 내려오면서 찾았던 것이 포인트임.  <br>
- dict을 두개를 사용하여 하나는 count를 세고, 하나는 새로운 pairdict을 만들어 pairdict에 들어있는 경우를 count함  <br>

5. Frequency Queries / 주어진 operation들로 (1-삽입, 2-있으면 삭제, 3-값확인, bool반환) 반환된bool값의 출력을 구하라
```python 
    # Terminated due to timeout :(    14/15 CORRECT
    def freqQuery(queries):
    d = {}
    ans = []
    for q in queries : 
        if q[0] == 1 : 
            d[q[1]] = d.get(q[1],0) +1 
        elif q[0] == 2 : 
            if d.get(q[1],0) : d[q[1]] -=1
        elif q[0] ==3 : 
            if any(d[k] == q[1] for k in d.keys()) : 
                ans.append(1)
            else : ans.append(0) 
    return ans 

    # completed all cases 
    def freqQuery(queries):
    d = {}
    ans = []
    for q in queries : 
        if q[0] == 1 : 
            d[q[1]] = d.get(q[1],0) +1 
        elif q[0] == 2 : 
            if d.get(q[1],0) : d[q[1]] -=1
        elif q[0] ==3 :
            if q[1] > len(queries) :
                ans.append(0)
                continue
            if any(d[k] == q[1] for k in d.keys()) : 
                ans.append(1)
            else : ans.append(0) 
    return ans 
```

### String Manipulation 
1. Strings: Making Anagrams / easy / 22min
```python 
    from collections  import Counter
    def makeAnagram(a, b):
        A = Counter(a)
        B = Counter(b)
        cnt = 0
        if A-B : 
            for v in (A-B).values():
                cnt += v
        if B-A : 
            for v in (B-A).values():
                cnt += v
        return cnt 
```

2. Sherlock and the Valid String / easy / 7min <br>
```python 
    def alternatingCharacters(s):
        s = list(s)
        stack = []
        cnt = 0
        while s : 
            i = s.pop(0)
            if not stack : 
                stack.append(i)
            else : 
                if i == stack[-1] :  
                        cnt +=1 
                else : stack.append(i)
        return cnt
```
- to change it into a string such that there are no matching adjacent characters.<br>
- to find the minimum number of required deletions.<br>

 3.  Sherlock and the Valid String / 문자열이 주어졌을 때 한가지의 문자를 삭제하여 모든 문자들이 동일한 갯수를 만들 수 있는가 / Medium / 쉬운 문제 였는데 오래 걸림<br>
```python 
    from collections import Counter
    def isValid(s):
        d = {}
        counter = Counter(s)
        for k,v in counter.items(): # k 는 문자 v는 숫자 
            d[v] = d.get(v,'') + k 
        print(d)
        if len(d) == 1: 
            return "YES"
        elif len(d) == 2 :
            #value길이가 하나밖에 없는키의 값을 -1 했을 때 0이 되거나 다른 키와 같아진다면 
            x = -1
            for k in d.keys(): 
                if len(d[k]) == 1 : 
                    x = k
                    break
            if x-1 == 0 or x-1 in d.keys():
                return "YES"
            else : return "NO"
        else : return "NO" 

    ########### 다른 코드 : 같은 방법인데, key1 , key2를 왜 저렇게 받을 생각을 못했냐 
        ,,,
        elif len(string.values())==2:
            key1,key2=string.keys()
            if string[key1]==1 and (key1-1==key2 or key1-1==0):
                print("YES")
            elif string[key2]==1 and (key2-1==key1 or key2-1==0):
                print("YES")
            else:
                print("NO")
        else:
            print("NO")

    print(isValid("aaaabbcc"))
    print(isValid("abcdefghhgfedecba"))
    print(isValid("ibfdgaeadiaefgbhbdghhhbgdfgeiccbiehhfcggchgghadhdhagfbahhddgghbdehidbibaeaagaeeigffcebfbaieggabcfbiiedcabfihchdfabifahcbhagccbdfifhghcadfiadeeaheeddddiecaicbgigccageicehfdhdgafaddhffadigfhhcaedcedecafeacbdacgfgfeeibgaiffdehigebhhehiaahfidibccdcdagifgaihacihadecgifihbebffebdfbchbgigeccahgihbcbcaggebaaafgfedbfgagfediddghdgbgehhhifhgcedechahidcbchebheihaadbbbiaiccededchdagfhccfdefigfibifabeiaccghcegfbcghaefifbachebaacbhbfgfddeceababbacgffbagidebeadfihaefefegbghgddbbgddeehgfbhafbccidebgehifafgbghafacgfdccgifdcbbbidfifhdaibgigebigaedeaaiadegfefbhacgddhchgcbgcaeaieiegiffchbgbebgbehbbfcebciiagacaiechdigbgbghefcahgbhfibhedaeeiffebdiabcifgccdefabccdghehfibfiifdaicfedagahhdcbhbicdgibgcedieihcichadgchgbdcdagaihebbabhibcihicadgadfcihdheefbhffiageddhgahaidfdhhdbgciiaciegchiiebfbcbhaeagccfhbfhaddagnfieihghfbaggiffbbfbecgaiiidccdceadbbdfgigibgcgchafccdchgifdeieicbaididhfcfdedbhaadedfageigfdehgcdaecaebebebfcieaecfagfdieaefdiedbcadchabhebgehiidfcgahcdhcdhgchhiiheffiifeegcfdgbdeffhgeghdfhbfbifgidcafbfcd"))
    print(isValid("aaaaabc"))
```

 4. ★★★ Special String Again / 스트링의 서브스트링 중 연속적으로 대칭적으로 생긴 스트링을 세는 문제. / Medium (Time complexity 개선하는 게 어려웠음.)<br>
```python 
    def substrCount(n, s):
    count = len(s) # 초기길이 
    for i, char in enumerate(s): # 캐릭터 하나씩 
        diff_char_idx = None # 다른 문자 인덱스 None 
        for j in range(i+1, n): # i 다음 인덱스부터 마지막 인덱스까지
            if char == s[j]: # char가 다음과 같으면 
                if diff_char_idx is None: # 다른 문자 인덱스가 비어 있으면 
                    count +=1 # 카운트 +1 
                elif j - diff_char_idx == diff_char_idx - i: 
                # 사이에 낀 인덱스인지 확인하는 코드이자 동시에 다음 인덱스가 또 
                # 동일하게 같을 때 diff가 존재하는지 체크함으로써 같으면 또 하나 
                # 더해줄 수있음 aa , aaa, aaaa 등 
                    count += 1
                    break
            else: # char가 s[j]와 다르면 
                if diff_char_idx is None: # 다른데 diff_char_idx가 None이면  
                    diff_char_idx = j # 넣어줘 
                else: # diff_char_idx가 이미 있으면  
                    break # braek해(왜냐면 이미 다른게 있는데 또 다르 거니까, 이번 turn은 버려야 하거든)
    return count

    def substrCount(n, s):
    count = 0
    count += n 
    for i, ch in enumerate(s): 
        dif = None 
        for j in range(i+1,n): 
            # 같은 경우
            if ch == s[j]:
                if dif is None : 
                    count += 1
                elif j-dif == dif-i : 
                    count += 1 
                    break  
            # 다른 경우 
            else : 
                if dif is None : # 다른 게 처음으로 나왔고 다음 탐색해야 
                    dif = j
                else : # 아예 망가진 경우  
                    break 
    return count
```
- common substring 구하는 문제인 듯. (하지만 longest가 아니고 모든 case )<br>
- https://en.wikipedia.org/wiki/Longest_common_substring_problem<br>
- 이렇게 구성하면 O(N*logN) N으로 겉에 한 번 돌고, 그 다음에는 range(i+1,n)으로 돌기 때문에 <br>

5. ★★★★Common Child / 두 개의 스트링이 주어졌을 때 연속X,순차적 둘다 존재하는 문자들의 최대개수 세기 / Medium (방법조차 떠오르지 않았음->DP문제)<br>
```python 
    # dynamic programming 으로 풀었는데, Terminated due to timeout 뜸 , 9/15 correct  / -> pypy3에서 돌리니까 통과됨
    def commonChild(s1, s2):
        arr = [[0 for _ in range(len(s2)+1)] for _ in range(len(s1)+1)]
        
        for row in range(len(s1)): 
            for col in range(len(s2)):
                if s1[row] == s2[col]:
                    arr[row+1][col+1] = arr[row][col]+1 
                else : 
                    arr[row+1][col+1] = max(arr[row][col+1], arr[row+1][col])
        return arr[-1][-1]
```
- https://en.wikipedia.org/wiki/Longest_common_subsequence_problem<br>
- The longest common subsequence (LCS) problem is the problem of finding the longest subsequence common to all sequences in a set of sequences (often just two sequences). <br>

### Sorting 
1. Sorting: Bubble Sort / easy / 13min <br>
```python 
    def swap(a,b) :
        tmp = a 
        a = b
        b = tmp 
        return a,b 
    def countSwaps(a):
        swaps = 0
        for i in range(len(a)): 
            for j in range(len(a)-(1+i)):
                if a[j] > a[j+1]: 
                    a[j], a[j+1] = swap(a[j], a[j+1])
                    swaps +=1 
        print(f'Array is sorted in {swaps} swaps.')
        print(f'First Element: {a[0]}')
        print(f'Last Element: {a[-1]}')
        return
```

2. Mark and Toys / 장난감의 가격이 주어지고 주어진 예산 하에 살 수 있는 최대 장난감 개수 return / easy (쉬움) / 7min<br>
```python 
    # Complete the maximumToys function below.
    def maximumToys(prices, k):
        sorted_prices = sorted(prices)
        t = 0
        c = 0
        while t <= k : 
            t += sorted_prices.pop(0)
            c +=1
        if c : c -=1 
        return c
```

3. Sorting: Comparator / name, score가 같이 input으로 들어오면 player라는 class로 받아서, 특정 조건에 맞게 sort 할 수 있도록 짜는 것 / Medium (쉬었음) / 미측정(오래안걸림)<br>
```python 
    from functools import cmp_to_key
    class Player:
        def __init__(self, name, score):
            self.name = name
            self.score = score
            
        # def __repr__(self): # 필요X (다들 지워서 짬)
            
        def comparator(a, b):
            if a.score < b.score : 
                return 1
            elif a.score > b.score : 
                return -1 
            elif a.score == b.score : 
                if a.name < b.name : 
                    return -1
                else : return 1
    n = int(input())
    data = []
    for i in range(n):
        name, score = input().split()
        score = int(score)
        player = Player(name, score)
        data.append(player)
        
    data = sorted(data, key=cmp_to_key(Player.comparator))
    for i in data:
        print(i.name, i.score)
```
4. ★★Fraudulent Activity Notifications / 지출 인덱스에서 trailing day d일 이후 사기 경고 문자가 전송되는 횟수를 계산하는 문제 <br>
```python 
    def activityNotifications(expenditure, d):
        if len(expenditure) <= d : 
            return 0 
        idx = d 
        count = 0 
        while idx <= len(expenditure)-1 : 
            data = sorted(expenditure[idx-d:idx]) #0,1,2,3,4
            med = None
            if len(data)%2 == 1: #01234  
                med = data[len(data)//2]
            else :
                med = (data[len(data)//2] + data[(len(data)//2)+1])/2 # 0123
            if expenditure[idx] >= med*2 : 
                count += 1
            idx += 1
        print(count)
        return

    def activityNotifications(expenditure, d):
        if len(expenditure) <= d : 
            return 0 
        idx = d 
        count = 0 
        data = []
        while idx <= len(expenditure)-1 : 
            # med 구하는 과정이 point 임 
            if not data : 
                data = [[i,expenditure[i]] for i in range(idx-d,idx)]
                data = sorted(data, key=lambda x: x[-1])
            # data = sorted(expenditure[idx-d:idx]) #0,1,2,3,4
            else : 
                data.append([idx-1, expenditure[idx-1]])
                data = sorted(data, key=lambda x : x[-1])
            print(f'{data}')
            med = None
            if len(data)%2 == 1: #01234  
                med = data[len(data)//2][-1]
            else :
                med = (data[len(data)//2][-1] + data[(len(data)//2)+1][-1])/2 # 0123
            if expenditure[idx] >= med*2 : 
                count += 1
            idx+=1
            data.remove(min(data))
        return count

    ##### 다른 사람 풀이 
    def get_limit(f,d):
        count = 0 
        m1,m2 = (d//2,d//2+1)
        m = []
        for i,j in enumerate(f):
            count+=j
            if not m and m1<=count:
                m.append(i)
            if m2<=count:
                m.append(i)
                break
        return m[-1]*2 if d%2 else sum(m)

    def activityNotifications(e, n, d):
        f = [0]*201
        count = 0
        for i in e[:d]: # d일 전까지 숫자 등장 횟수를 셈 
            f[i]+=1
        for i,v in enumerate(e[d:]):
            limit = get_limit(f,d)
            if v>=limit:
                count+=1
            f[v]+=1
            f[e[i]]-=1
        return count
    n,d = map(int,input().split())
    e = list(map(int,input().split()))
    print(activityNotifications(e, n, d))
    # 총 expenditure가 0~200이라는 것을 이용하여 모든 expenditure를 인덱스로 만들어 0을 채운 뒤 하나씩 이동할 때마다 1로 바꿔줬음
```
- d일 바로 이전까지의 지출내역들 중 median*2 <= expenditure[d]이면 경고문자 발송 <br>
- 역시 관건은 time complexity <br>
- counting sort를 사용해서 푸는 문제인데 다시 들여다 봐야함 .<br>

### Greedy Algorithms 
1. Minimum Absolute Difference in an Array / 주어진 배열에서 임의의 두 값을 골라 계산될 수 있는 최소 절댓값을 찾아라. / easy <br>
```python 
    from itertools import combinations 
    def minimumAbsoluteDifference(arr):
        sorted_arr = sorted(arr)
        bucket = []
        for i in range(len(arr)-1):
            if not bucket : 
                bucket.append(abs(sorted_arr[i]-sorted_arr[i+1]))
            else : 
                if bucket[0] > abs(sorted_arr[i]-sorted_arr[i+1]): 
                    bucket.pop()
                    bucket.append(abs(sorted_arr[i]-sorted_arr[i+1]))
        return bucket[0] 

    ##### another solution 
    n,a = input(),sorted(map(int, input().split()))
    print(min(abs(x-y) for x,y in zip(a,a[1:])))
```
### Search
1. ★★★Hash Tables: Ice Cream Parlor / 아이스크림 가게에서 주어진 예산에 맞게 사 먹을 수 있는 2가지 아이스크림의 인덱스 추출 / Medium / <br>
```python 
    from collections import Counter 
    def whatFlavors(arr, money):
        costs = Counter(arr)
        half = money/2
        comb = set()
        for cost in costs : 
            if (cost!=half and money-cost in costs) or (cost==half and costs[cost]>1): 
                comb.add(cost) # set구조의 add는 순차적으로 들어감
                print("comb set : ",comb)
        # print("comb set : ",comb)
        for idx, c in enumerate(arr, 1): 
            if c in comb : 
                yield idx 
                # yield쓰면 generator가 생성됨. 
                # return과 유사한데 generator로 계속 iter된다고 생각하면 됨 
                
    print(*whatFlavors([7, 2, 5, 4, 11], 12))
```
- Counter로 counting 이후 , 아이템들을 set에 넣고 (set에 넣으면 sort되며 들어감) / 그걸을 초기 arr에서 찾아서 index yield해준다. <br>


- Interview kit
    - Arrays (4/5)

    - Dict and Hashmaps (5/5) (solved all)
    - String Manipulation (5/5) (solved all)
    - Sorting (3/5)

    - Greedy Algorithms (1/5)
    - Search (1/5)
    - Dynamic Programming (0/4)

    - Stacks and Queues 
    - Graphs 
    - Trees 
    - Linked Lists 
    - Recursion and Backtracking 
    - Miscellaneous


