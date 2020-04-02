---
layout: post
title: "슬라이딩 윈도우(Sliding Window)"
summary : 순서대로 움직이는 고정된 크기의 부분 배열
date: 2020.03.15 10:00:00 +0900
---

### __슬라이딩 윈도우__ 
> 순서대로 움직이는 고정된 크기의 부분 배열

### 특징

* 네트워크 호스트간의 패킷의 흐름을 제어하기 위한 알고리즘이다.
* 고정된 크기의 부분 배열에서 최솟값을 찾는데 사용할 수도 있다.

### Example

<div>
	<img width="100%" alt="sliding_window" src="https://user-images.githubusercontent.com/17156386/74204746-c5d4b880-4cb7-11ea-8ac5-3b56c9968978.png">
</div>

크기가 4인 부분배열이 왼쪽부터 오른쪽으로 차례대로 이동하는 것을 알 수 있다. 
<br>네트워크 호스트간의 패킷 흐름을 제어하기 위해 사용하나 구간 최소값을 연속적으로 찾아내는 문제에 활용될 수도 있다.

### 풀이방법

1. 원소의 인덱스와 값을 저장하는 덱을 만든다.
```c++
#include <deque>
#define pii pair<int,int>

deque<pii> window;
```

2. 값을 입력받아 이 값보다 큰 원소들을 덱에서 제거해 준다.
```c++
int cur; cin>>cur;
while(!window.empty() && window.back().second >= cur){
	window.pop_back();
}
```

3. 부분배열 범위를 벗어난 앞 원소를 제거해준다.
```c++
if(window.front().first + l <= i) window.pop_front();
```

### 문제

<a href = "https://www.acmicpc.net/problem/11003" target = "_blank">백준 11003:최솟값 찾기</a>

```c++
#include <iostream>
#include <deque>
#define pii pair<int,int>
using namespace std;
int main(){
	ios_base::sync_with_stdio(false); cin.tie(NULL);
	int n,l; cin>>n>>l;
	// 원소의 인덱스와 값을 저장할 덱을 사용
	deque<pii> window;
	for(int i=0,cur;i<n;i++){
		cin>>cur;
		// 값을 입력받고 입력받은 값보다 큰 원소들을 제거
		while(!window.empty() && window.back().second >= cur){
			window.pop_back();
		}	
		// 현재 입력받은 값을 넣어준다.
		window.push_back(make_pair(i,cur));
		// 부분배열의 범위를 벗어난 원소를 제거해 준다. 
		if(window.front().first + l <= i) window.pop_front();
		cout<<window.front().second<<' ';
	}
}
```
