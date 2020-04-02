---
layout: post
title : "투 포인터 (Two Pointer)"
description: 포인터 두 개를 이용하여 배열을 효율적으로 탐색하는 방법
---
### 투 포인터(Two Pointer)
> 포인터 두 개를 이용하여 배열을 효율적으로 탐색하는 방법

### 특징
* n개로 이루어진 배열과 합이 x인 부분배열을 찾기 위한 용도로 주로 사용한다.
* 배열을 탐색할 경우 두개의 포인터는 모두 한쪽 방향으로 움직인다.

### Example
<div>
	<img width="100%" alt="two_pointer1" src="https://user-images.githubusercontent.com/17156386/74104042-3da9c280-4b94-11ea-99a0-c2303c5fad52.png">
</div>
두 포인터 사이에 존재하는 값들의 합이 x보다 작으면 오른쪽 포인터를 오른쪽으로 이동시키고, x값 보다 크면 왼쪽 포인터를 오른쪽으로 이동시켜 합을 검사한다.

### 풀이방법

1. 왼쪽,오른쪽 포인터가 배열의 첫번째 인덱스를 나타내도록 한다.
```c++
for(int l=0,r=0,sum=0;r<n;r++)
```

2. 부분합의 값이 찾는 값보다 크다면 부분합이 찾는값 이하가 될때까지 왼쪽 포인터를 이동시켜 준후 찾는값과 비교한다.
```c++
while(sum > m){
	sum -= num[l];
	l++;
}
if(sum == m)ans++;
```

### 문제
<a href="https://www.acmicpc.net/problem/2003" target = "_blank">백준 2003:수들의 합2</a>
```c++
#include <iostream>
#include <vector>
using namespace std;
int main(){
	ios_base::sync_with_stdio(false); cin.tie(NULL);
	int n,m,ans=0,sum=0; cin>>n>>m;
	vector<int> num(n);
	for(int l=0,r=0;r<n;r++){
		// 원소의 값을 하나씩 입력받으면서 검사
		cin>>num[r]; sum+=num[r];
		// 부분합이 찾는값 보다 크다면 왼쪽 포인터를 이동시킨다.
		while(sum > m){
			sum-=num[l];
			l++;
		}
		// 부분합이 찾는값과 같다면 카운트 해준다.
		if(sum == m) ans++;
	}
	cout<<ans;
}
```
