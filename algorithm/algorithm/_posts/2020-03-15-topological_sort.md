---
layout: post
title: "위상정렬 (Topological Sort)"
description: 방향 그래프 노드들의 순서를 정해주는 것
---
### 위상정렬(Topological Sort)
> 방향 그래프 노드들의 순서를 정해주는 것

### 특징
* 노드 a 에서 노드 b 로의 경로가 존재하면 a는 b보다 앞에 나와야 한다.
* **DAG** 인 경우 항상 위상정렬이 가능하다( **DAG**( Directed Acyclic Graph ) : 사이클이 없는 방향그래프)

## Example 

<div>
	<img width="100%" alt="topological_sort01" src="https://user-images.githubusercontent.com/17156386/74046379-cd733380-4a11-11ea-991b-7b408adcb9a4.png">
</div>

위 방향 그래프는 사이클이 존재하지 않는 방향 그래프 이므로 위상정렬이 가능하다
<br> 순서는 1번 노드가 가장 앞에 나오고 3번이 2번보다 앞에 있기 때문에 두번째 로는 3번 노드가 세번째로는 2번 노드가 마지막으로 4번 노드가 위치하게 된다. 
<br> 순서 : [1 -> 3 -> 2 -> 4]

### 풀이방법

1. 노드의 개수를 V, 간선의 개수를 E라고 하였을때 노드에 연결된 간선의 정보와 해당 노드로 들어오는 간선의 개수를 저장하는 배열을 만들어준다(a->b 간선이 존재할 때, 이 간선의 a에서 나와서 b로 들어간다).
```c++
#define vi vector<int>
vector<vi> edge(V);
vector<vi> edge_num(V);
```

2. 노드를 탐색하면 연결된 간선의 개수가 0개인 노드를 큐에 넣어준다.
```c++
queue<int> que;
for(int i=0; i<V; i++){
	if(!edge_num[i]){
		que.push(i);
	}
}
```

3. 큐에서 원소를 하나씩 빼내며  연결된 간선을 삭제한 후, 간선으로 연결된 노드에 들어오는 간선의 개수가 0인 경우 큐에 넣어준다.(큐에 원소가 존재하지 않을때까지 반복)
```c++
while(!que.empty()){
	int cur = que.front();
	que.pop();
	for(int i=0; i<edge[cur].size(); i++){
		int next = edge[cur][i];
		if(--edge_num[next] == 0){
			que.push(next);
		}
	}
}
```

### 문제
<a href = "https://www.acmicpc.net/problem/2252" target = "_blank">백준 2252:줄 세우기</a>

```c++
#include <iostream>
#include <queue>
#include <vector>
#define vi vector<int>
using namespace std;

//간선의 정보를 저장할 edge, 개수를 저장할 edge_num 배열
vector<vi> edge;
vector<int> edge_num;
queue<int> que;

int main(){
	ios_base::sync_with_stdio(false); cin.tie(NULL);
	int V,E; cin>>V>>E;

	//배열의 크기 초기화
	edge = vector<vi>(V);
	edge_num = vector<int>(V);

	for(int i=0,a,b;i<E;i++){
		cin>>a>>b;
		// a 노드에서 b 노드로 가는 경로가 존재
		edge[a-1].push_back(b-1);
		edge_num[b-1]++;
	}

	for(int i=0;i<V;i++){
		if(!edge_num[i])que.push(i);
	}

	while(!que.empty()){
		int cur = que.front();
		que.pop();
		cout<<cur+1<<' ';
		
		// 간선 제거한 후 들어오는 간선의 개수가 0개인지 확인
		for(int i=0;i<edge[cur].size();i++){
			int next = edge[cur][i];
			if(--edge_num[next] == 0){
				que.push(next);
			}
		}
	}
}
```
