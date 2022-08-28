# 최단 경로 탐색 (Find Shortest Path)

최단 경로 탐색 알고리즘은 주어진 그래프 (or 맵)에서 시작점을 기준으로 각각의 도착점으로 가는 최단 경로를 탐색하는 알고리즘을 지칭합니다.

저는 대표적인 최단 경로 탐색 알고리즘인 다익스트라와 플로이드 와샬 알고리즘에 대해 정리해 보도록 하겠습니다.

1. [다익스트라 (Dijkstra)](#다익스트라-dijkstra)
    1. [다익스트라란?](#다익스트라란)
    2. [동작 과정](#동작-과정)
    3. [알고리즘의 흐름 (글로 정리)](#알고리즘의-흐름)
    4. [구현 소스 코드 (with C++)](#구현-소스-코드-with-c)
2. [플로이드-와샬 (Floyd-Warshall)](#플로이드-와샬-floyd-warshall)
    1. [플로이드 와샬이란??](#플로이드-와샬이란)
    2. [알고리즘의 흐름 정리](#알고리즘-흐름-정리)
    3. [구현 소스 코드 (with C++)](#알고리즘-구현-소스-코드-with-c)

-----------------

## 다익스트라 (Dijkstra)

### 다익스트라란??

다익스트라 알고리즘은 대표적인 최단 경로 탐색 알고리즘 중 하나로 그래프 상에서 하나의 노드를 기점으로 다른 노드로 가는 최단 경로를 탐색하는 알고리즘입니다.

간단하게 말해서 다익스트라를 이용하면 그래프 상의 한 노드에서 출발했을 때, 다른 모든 노드로의 최단 경로를 구할 수 있습니다.

다만, 다익스트라를 사용하는 경우 그래프에 **음의 간선이 포함되면, 최단 경로 탐색이 불가능하다는 점을 유의해야** 합니다!!

### 동작 과정

다익스트라 알고리즘의 동작 과정 설명을 위해 다음과 같은 그래프를 예시로 들어보겠습니다.

![image](https://postfiles.pstatic.net/MjAyMjA3MThfMjE1/MDAxNjU4MTI5MDE0NTYy.aXRqyJWvNYzLY_TnCq2MBa50QTtgyZ6ccTNsESrUnZQg.00zGGa50vsg9cR1r9A9UBZ4ksUiVItABh7fJkB68l4Ag.PNG.book541/image.png?type=w773)

| 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| 1 |   |   |   |   |   |

시작 지점을 1번 노드라고 생각하고, 위 그래프에서 다익스트라 알고리즘에 따라 최단 경로를 찾아가는 방식을 설명해 보도록 하겠습니다. 

![image](https://postfiles.pstatic.net/MjAyMjA3MThfMTYx/MDAxNjU4MTI5MDk3NjM2.HuNg4NATvPyCWzhssRro4FpyKPb7tstooGEsUCNCW5Yg.1TftnmOOa3hg88zF-Bo3ixZru0UJ3yDbq6teCMRBHdAg.PNG.book541/image.png?type=w773)

1번 노드를 우선 방문한 후에 인접한 노드인 2, 5번 노드에 대해서 최단 경로를 갱신해 줍니다. 1번 노드와 인접한 두 개의 노드는 아직 한 번도 방문한 적이 없기 때문에, 각각 3, 5로 최단 경로에 대한 거리가 갱신됩니다.

| 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| 1 | 3 |   |   | 5 |   |

다음으로 2번 노드의 인접한 노드에 대해서 최단 경로를 갱신합니다.

![image](https://postfiles.pstatic.net/MjAyMjA3MThfNDMg/MDAxNjU4MTI5MTk2NDk3.xA9BHYKn8B49xHz7ISMuFvVS0XOfzPQBuql4hzXfk8Mg.P63Kd-LCPTTPKUbpQ2B75mAdar9blCPe66nXlAB25HMg.PNG.book541/image.png?type=w773)

2번 노드는 3번 노드, 4번 노드와 인접하고, 두 개의 노드 또한 한 번도 방문하지 않은 노드이기 때문에, 최단 경로를 각각 3 + 3 = 6, 3 + 5 = 8로 갱신합니다.

| 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| 1 | 3 | 6 | 8 | 5 |   |

다음으로 5번 노드의 인접 노드에 대해서 최단 경로를 갱신합니다. 

![image](https://postfiles.pstatic.net/MjAyMjA3MThfMjIg/MDAxNjU4MTI5NTA1Nzkz.eLLWNJ1sFhjT4f8_bG4z4R4Qi1BYUf472f6Ui8nLhc4g.G0rDPdBCSy02p5VMEbYUvW3tM8OZ704sFmNMD4Q2ZSYg.PNG.book541/image.png?type=w773)

5번 노드는 4, 6번 노드와 인접해있고, 5번 노드를 거쳐서 4, 6번 노드에 가는 경우 각각 5 + 1 = 6, 5 + 5 = 10의 거리만큼 이동해야 합니다.

| 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|
| 1 | 3 | 6 | 8 > 6 | 5 | 10  |

이는 기존에 4번 노드로 갈 때의 거리인 8보다 짧기 때문에, 4번 노드로 가는 거리를 갱신하고, 6번 노드의 경우 기존에 방문하지 않은 노드이므로 최단 거리를 10으로 갱신해 줍니다. 

대강 이런 방식으로 그래프를 탐색하면서 최단 경로를 구하는 알고리즘이 다익스트라 알고리즘입니다. (마지막까지 설명하지는 않았으나 위 결과대로 최단 경로를 구할 수 있습니다.)

위 그래프는 사실 방향이 있는 그래프 (directed-graph 또는 유향 그래프라고 부릅니다.)이기도 하고, 4번 노드 이외에는 이후에 최단 거리가 갱신되지 않기 때문에, 다익스트라에 대해 완전히 이해하기 어렵기 때문에, 글로 정리해서 다익스트라 알고리즘에 대해서 설명하겠습니다.

### 알고리즘의 흐름

1. 시작 노드를 기준으로 모든 노드에 대한 최단 거리를 저장하는 배열을 초기화한다. (일반적으로 최댓값으로 갱신해 줍니다.)
2. Heap 자료 구조(priority queue)에 시작 노드를 넣어줍니다. (최소힙을 사용합니다. 이는 다음 방문할 노드를 최솟값을 우선으로 방문하기 위함입니다.)
3. Heap이 빌 때까지 while 문을 반복합니다.
4. Heap의 head에 해당하는 노드의 인접한 노드(연결되어 있는 노드)에 대해서 현재 노드를 거쳐 가는 경우 최단 거리가 갱신되는지 판단합니다.
5. 최단 거리가 갱신되면 Heap에 해당 인접 노드를 넣어줍니다.
6. 3번 ~ 6번 과정으로 while 문이 끝날 때까지 반복합니다.

글로 쓰고 보니 또 복잡하게 느껴지는데, 간단하게 말하면 현재 노드를 거쳐 인접한 노드를 방문할 때 기존의 최단 거리가 갱신된다면? 인접한 노드의 인접한 노드 또한 똑같이 최단 거리가 갱신되는지 확인하면서 전체 그래프에 대한 최단 거리를 찾는다라고 할 수 있을 것 같습니다.

Heap 또는 Priority Queue 자료 구조를 사용하는 이유는 매번 현재 시점에서 최단 거리가 갱신된 노드 중에서 가장 거리가 짧은 경우를 뽑기 위해서이고, 자료 구조가 빌 때까지 반복하는 이유는 모든 노드로의 경로가 최단거리이면, 자료 구조에 새로운 노드가 push 될 수가 없기 때문입니다!

다익스트라 알고리즘은 Dynamic programming(동적 프로그래밍) 기법을 활용해서 구현하기 때문에, 간단하고 빠르게 구현할 수 있고, 최단 거리를 찾을 때 효율적인 알고리즘이기 때문에, 꼭 알아둬야 하는 알고리즘이라고 생각합니다.

### 구현 소스 코드 (with C++)

위에 설명한 내용을 바탕을 소스 코드를 간단하게 짜봤습니다. 언어는 C++를 이용해서 구현해 봤습니다.

```c
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int n, m; // 노드의 개수, 간선의 개수
int INF = 1000000000;

// edge data
vector<pair<int, int>> a[7]; // pair<end point, distance>
// 그래프 내의 모든 노드로의 최단 경로를 저장한다.
int d[7];

void dijkstra(int start) {
	d[start] = 0;
	priority_queue<pair<int, int>> pq; // heap structure <distance, end point>
	pq.push(make_pair(0, start));

	while (!pq.empty()) {
		int cur = pq.top().second; // shortest path's index in heap
		// 짧은 길이가 가장 위로 저장될 수 있도록 음수의 형태로 저장하자!
		int distance = -pq.top().first;
		pq.pop();

		// 이미 shortest path가 아닌 경우 skip
		if (d[cur] < distance) continue;

		// 선택된 노드의 인접 노드를 이용하여 최소 거리를 갱신하는 for loop
		for (int i = 0; i < a[cur].size(); i++) {
			int next = a[cur][i].first;
			int next_distance = a[cur][i].second + distance;

			if (d[next] < next_distance)
				continue;

			d[next] = next_distance;
			// same with pq.push(make_pair(next, -next_distance));
			pq.push({ -next_distance, next });
		}
	}
}

int main() {
	cin >> n >> m;

	// 모든 최단 경로의 거리를 INF로 초기화
	for (int i = 1; i <= n; i++) {
		d[i] = INF;
	}

	for (int i = 0; i < m; i++) {
		int start, end, distance;
		cin >> start >> end >> distance;

		a[start].push_back({ end, distance });
	}

	dijkstra(1); // 1번 노드에서 시작한다.

	for (int i = 1; i <= n; i++) {
		cout << i << "번째 노드로의 최단 경로: " << d[i] << "\n";
	}

	return 0;
}
```

priority_queue 자료 구조를 이용해서 heap을 대체했으며, priority_queue 자료 구조가 기본적으로 내림 차순으로 정렬하여 요소들을 저장하기 때문에, 거리에 음의 부호를 붙여서 자체적으로 오름 차순으로 값을 사용할 수 있도록 구현했습니다.

위 코드를 실행하고 아래의 입력을 넣으면 다음과 같이 출력됩니다!


### 실행 결과!!
```
﻿입력:
6 7
1 2 3
1 5 5
2 3 3
2 4 5
5 4 1
5 6 5
6 3 1

출력:
1번째 노드로의 최단 경로: 0
2번째 노드로의 최단 경로: 3
3번째 노드로의 최단 경로: 6
4번째 노드로의 최단 경로: 6
5번째 노드로의 최단 경로: 5
6번째 노드로의 최단 경로: 10
```

## 플로이드 와샬 (Floyd-Warshall)

### 플로이드 와샬이란??

플로이드-와샬 알고리즘은 앞서 정리한 다익스트라 알고리즘과는 다르게 그래프 내의 모든 정점(node)으로부터 모든 정점으로의 최단 경로를 찾기 위해 사용하는 알고리즘입니다.

다익스트라와는 다르게 음의 간선(edge)가 있어도 최단 경로 탐색이 가능하지만, 음의 사이클(cycle)이 있는 경우에는 최단 경로 탐색이 불가능한 점을 유의해야 합니다.

플로이드 와샬 알고리즘의 경우 dynamic programming(동적 계획법) 기법을 사용해서 구현하며, 시간 복잡도의 경우 그래프의 노드 개수가 N 개라고 가정했을 때, O(N^3)의 시간 복잡도를 갖습니다.

플로이드 와샬 알고리즘의 핵심 개념은 "이 정점을 거쳐가는 경우와 거쳐가지 않는 경우 중 어떤 경우가 더 최단 거리일까?"입니다. 

### 알고리즘 흐름 정리

아래의 그래프를 예로 들어서 설명해 보겠습니다!!

![image](https://postfiles.pstatic.net/MjAyMjA3MTlfMTU0/MDAxNjU4MjE4MDA4MjAy.BS7nrExPe_dQTnU5NgCUdwHVcyz3G5U9P-_P8ssbJtEg.7LeOMvAUo8J30kcgn89J28JRYop8degJodqLQl5eEtYg.PNG.book541/image.png?type=w773)

예시 그래프에 따라 간선에 따른 정점의 연결 정보를 아래와 같이 표기할 수 있습니다. 

| 0 | 3 | 11 |
|---|---|---|
| 6 | 0 | 2 |
| 3 | x | 0 |

앞으로 이 배열(A라고 부르겠습니다.)은 각 출발점에서 도착점으로의 최단 거리를 표현하게 될 것이며, 매 단계마다 이 배열을 갱신해서 최종적으로 모든 출발점에서 도착점으로의 최단 경로에 대한 거리를 구할 수 있게 될 것입니다.

위 배열을 보면 대각선의 영역이 0으로 초기화된 것을 확인할 수 있는데, 이는 자기 자신으로 가는 경로에 대해서는 0으로 생각하기 때문입니다.

이제 1번 노드부터 거쳐서 가는 경우를 생각하며 최단 경로를 갱신해 보도록 하겠습니다. 


​① 1번 노드를 거쳐가는 경우

이번 단계에서는 모든 경로에 대해 1번 노드를 거쳐가는 경우가 더 빠른지 아니면, 기존의 경로가 더 빠른지에 대한 비교를 진행합니다. 

=> i = 1 ~ 3, j = 1 ~ 3 인 경우

i에서 j로 갈 때  1을 경유하는 경우 vs 기존의 i에서 j로 가는 최단 경로

=> i에서 1로 가는 경로 + 1에서 j로 가는 경로 vs 기존의 i에서 j로 가는 최단 경로

간단하게 풀면, 위의 비교를 모든 i, j에 대해서 실행하게 되는 것입니다. 

| 0 | 3 | 11 |
|---|---|---|
| 6 | 0 | 2 |
| 3 | x | 0 |

위 배열을 다시 참고해서 비교를 진행하면 

A[3][2] = null vs A[3][1] + A[1][2] = 3 + 3 = 6

위 경우에 대해서 기존에는 경로가 존재하지 않았던 3번 노드에서 2번 노드로 향하는 경우 6으로 초기화할 수 있게 되어 아래와 같이 배열 A가 갱신됩니다.

| 0 | 3 | 11 |
|---|---|---|
| 6 | 0 | 2 |
| 3 | x -> 6 | 0 |

② 2번 노드를 거쳐서 가는 경우

이번 과정도 앞선 과정과 동일하게 진행되며, 이번에는 기존의 "1번 노드 -> 3번 노드"에 대한 최단 거리인 11을 다음과 같이 갱신하게 됩니다.

A[1][3] = 11 vs A[1][2] + A[2][3] = 3 + 2 = 5

| 0 | 3 | 11 -> 5 |
|---|---|---|
| 6 | 0 | 2 |
| 3 | 6 | 0 |

③ 3번 노드를 거쳐서 가는 경우

이번에는

A[2][1] = 6 vs A[2][3] + A[3][1] = 2 + 3 = 5

위의 경우에서 최단 거리를 갱신할 수 있기 때문에 다음과 같이 표가 갱신되며 플로이드 와샬 알고리즘을 이용한 최단 거리 갱신이 마무리됩니다.

| 0 | 3 | 5 |
|---|---|---|
| 6 -> 5 | 0 | 2 |
| 3 | 6 | 0 |

### 알고리즘 구현 소스 코드 (with C++)

C++ 언어를 이용해서 플로이드 와샬 알고리즘을 아래와 같이 간단하게 구현할 수 있습니다. 

```c
#include <iostream>
#define INF 10000001

using namespace std;

int n = 3;

int a[3][3] = {
	{0, 3, 11},
	{6, 0, 2},
	{3, INF, 0}
};

void floydWarshall() {
	// initialize result array
	int d[3][3];

	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			d[i][j] = a[i][j];
		}
	}

	// k = 거쳐가는 노드
	for (int k = 0; k < n; k++) {
		// i는 시작점
		for (int i = 0; i < n; i++) {
			// j는 도착점
			for (int j = 0; j < n; j++) {
				// k를 거쳐가는 경우가 더 최단거리인 경우 갱신한다.
				if (d[i][k] + d[k][j] < d[i][j]) {
					d[i][j] = d[i][k] + d[k][j];
				}
				/*
				d[i][j] = (d[i][j] > d[i][k] + d[k][j]) ? d[i][k] + d[k][j] : d[i][j];
				*/
			}
		}
	}

	// print result (전체 최단 경로)
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			printf("%d ", d[i][j]);
		}
		printf("\n");
	}
}

int main() {
	// call floyd-warshall algorithm function
	floydWarshall();

	return 0;
}
```

```
프로그램 출력:

0 3 5
5 0 2
3 6 0
```