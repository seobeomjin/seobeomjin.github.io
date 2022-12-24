---
layout: post
title: C++ 내가 보려고 정리하는 syntax 정리 
subtitle: C++ syntax 와 관련하여 정리합니다.
categories: Study
tags: c++ coding-test
comments: True
published: True
---

- strcpy 
```cpp 
char[11] name
void copy_str(char* str){    // char[11] 이라도 입력은, char의 시작 포인터 
    strcpy_s(name, str);// name 이 복사될 곳, str이 변수 
    // char[] 에 복사되도록.
}
// 변수명은 strcpy , 그 입력은 모두 char[] 배열
```

- int,int pair 형 변수 정의 
```cpp
#define pii pair<int, int> 
```

- set 에 대한 iterator 변수를 받아옴 & set 에 insert 
```cpp
auto bg = set_.begin(); 
if (bg->first == 1) 
    s.insert({ ret + 1, bg->second }); // 해당하는 pair 정보를 set에 넣음 
```

- set compare 함수 만들기 
```cpp
struct compare{
    bool operator() (const pii &a, const pii &b) const
    { return a < b; }
}
```

- dijkstra pseudo code <br>
```cpp 
//init
visited [] = false 
dist[] = INF 

dist[출발지] = 시작값 

for i // 1st FOR
    minCost = INF 
    minIndex = -1 
    for j // 2nd FOR
        if( !visited[j] && minCost > dist[j] )  // minCost GET
            minCost = dist[j] 
            minIndex = j 
    break condtions // (minCost == INF || minIndex == 도착지)  // break CONDITION

    visited[minIndex] = true // visit check ★

    for j  //dist update based on till minIndex !
        dist[j] = min (dist[j] , minCost + edge[minIndex][j] ) 
```

- Union Find pseudo code 

