# 그래프 탐색 (Graph Search)

0. 그래프 탐색 그리고 그래프에 대해서
1. DFS (Depth-First Search)
2. BFS (Breadth-First Search)

## 그래프 탐색이란

그래프가 주어졌을 때, 하나의 정점을 시작으로 하여 그래프 내의 다른 모든 정점들을 방문하는 것을 의미한다. 

대표적으로 BFS, DFS 두 가지의 그래프 탐색 기법이 존재한다.

## 그래프란?

여기서 정리할 DFS, BFS는 그래프를 탐색하는 방법에 대한 개념입니다. 따라서 그래프에 대해 간단하게만 설명하겠습니다.

그래프는 정점과 간선으로 이루어진 자료 구조로 정점은 그래프를 이루는 하나하나의 지점들을, 간선은 이러한 정점들의 연결 관계를 표현하는 것을 의미합니다.

![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMTA3/MDAxNjUxNjY1ODgyNzg1.e5OJdZBe2Pj0ulDPiEzF9I5JHD-T4HwTY0D_XU3lwQwg.Lv4zvuGTb5PV37gMb_sfaQPYxhaWT8QdpHRU8Gu_rRYg.PNG.book541/image.png?type=w773)

위와 같은 예시 그림도 그래프의 일종이라고 볼 수 있습니다. (정점은 1, 2, 3, 4 그리고 1번과 2번 정점을 연결하는 간선, 2번과 3번, 3번과 5번 정점을 연결하는 간선으로 구성됩니다.)

## DFS란?

DFS는 Depth-First Search의 약자로 깊이 우선 탐색이라는 이름으로 불립니다. 이름 그대로 깊이 우선 탐색 방식은 현재 탐색하고 있는 경로를 끝까지 탐색한 다음 다른 경로를 탐색한다는 것을 의미하는데, 그림을 통해 정리하면 다음과 같습니다. 

![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMTEw/MDAxNjUxNjY2ODk2OTQ4.6LfeNwf4qxByGB9UJM9Z7cDkF3z9o663lv1gQUD3Ij8g.xXl3igbRGBiugT2xWMoLwjfKxKV9zY3t4dXl7n-nUkog.PNG.book541/image.png?type=w773)

위 그래프가 초기 상태라고 했을 때 DFS 방식으로 탐색을 한다면, 아래와 같은 순서대로 탐색을 진행합니다.

![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMTQx/MDAxNjUxNjY4NzEwNDAz.NlNTqmxioGqnz_2qEfTH7BtEKXZMIQF-9mvpYSLUSPsg.I1uymkuSYob1m-vE99aL6gavd-QvwmskXKaiBmYmT30g.PNG.book541/image.png?type=w773)


![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMTAg/MDAxNjUxNjY4Nzk2MjY3.BOV0v1zczHTGFrVXGFdTKIUKkYyFEv1Ml3HWCPuVRb8g.Q8Xl_Q8bGQsHcJfp4n8DXIvuvrQwZp1nyx7mrDeXXbkg.PNG.book541/image.png?type=w773)


![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMTEw/MDAxNjUxNjY4ODQwNDE2.-iyhE2AVA4f5HsUOysBrP7OhcCrEUK5z4Nf5nHZOdXUg.qmi9E-hKzTr6j2sVEcSYe7b0FpXa9qeTmMgEntemw3Eg.PNG.book541/image.png?type=w773)

여기서 3이 아닌 4를 고른 이유는 특별히 없습니다. 어떤 정점을 먼저 방문하는지는 구현에 따라 달라지기 때문에, 경우에 따라서 3번 정점을 먼저 방문할 수도 있습니다!

![image](https://postfiles.pstatic.net/MjAyMjA1MDRfNDIg/MDAxNjUxNjY4ODgxMjI1.ip_0phv_XJSybW4QeFsNKLNRtYtQySy2LOqDH_STGEYg.XYbh2DW6fKEWCwaT7nduUV-NsdPv7bk-XG6apJcDB20g.PNG.book541/image.png?type=w773)



![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMjEy/MDAxNjUxNjY4OTE2ODYy.rueugSDBQNigAKPBmQrmnc0uP1Ni6Qjk0-z7E6VXMGcg.NjXSx9FAFbECrajSmiTuWY8TetkTUL5t59Cu_73Lyegg.PNG.book541/image.png?type=w773)

위와 같이 6번까지 방문을 했는데, 6번 이후에는 더 이상 방문할 정점이 없어서 아래와 같이 2번까지 되돌아가서 2번 정점과 인접한 3번 정점을 방문합니다!

![image](https://postfiles.pstatic.net/MjAyMjA1MDRfMjEx/MDAxNjUxNjY4OTU2MTQy.GQxqM1qBWNpwaDVo8MXIJDGF4xEkwrT0CBIJBEt8B_4g.gygkVSVBCND2Tda_WIYIS2kymBsXEtZ3d2xaO-Fg5A0g.PNG.book541/image.png?type=w773)

2번으로 다시 돌아와 3번 정점을 방문했기 때문에, 색깔을 조금 진하게 칠해서 표현해 봤습니다.

## DFS 구현 방법

DFS는 2가지 방법으로 구현할 수 있습니다. 

1. 재귀함수를 이용한 구현
2. stack 자료구조를 이용한 구현

저는 C++ 언어를 이용해 DFS 방식으로 그래프를 탐색하는 코드를 작성해 봤습니다. 재귀 함수를 이용하는 방법과 stack 자료 구조를 사용하는 방법으로 DFS를 구현할 수 있는 이유는 재귀 함수의 동작 방식을 살펴보면 쉽게 이해할 수 있습니다.


DFS 방식은 현재 방문한 노드의 인접 노드 중 하나로 바로 방문을 하는 방식을 취해 그래프를 탐색합니다. 재귀 함수는 함수의 수행 중에서 동일한 함수를 또 다시 호출하는 방식으로 이루어 지는데, 바로 이 점을 이용해서 현재 노드와 인접한 노드에 대해서 DFS 함수를 바로 호출하는 방식으로 코드를 구현하면, 재귀 함수를 이용해 DFS 탐색을 구현할 수 있는 것입니다.

코드는 아래와 같이 작성할 수 있습니다.

```c
vector<int> v[MAX];
bool visited[MAX];

int res = 0;

void dfs(int idx) {
    for (int i = 0; i < v[idx].size(); i++) {
        int next_idx = v[idx][i];
        if (!visited[next_idx]) {
            visited[next_idx] = true;
            res++;
            dfs(next_idx);
        }
    }
    return;
}
```
dfs 라는 함수가 재귀적 호출을 하면서 DFS 방식으로 그래프를 탐색하는 코드의 일부입니다. v라는 vector 자료 구조를 이용해서 간선 정보를 저장하고, visited 배열을 이용해서 각 정점의 방문 여부를 판단합니다.

​
dfs 함수에서는 다음 정점으로 이동해 dfs 함수를 실시하기 이전에 현재 정점에 대한 방문 처리를 진행 한 후에 다음 함수의 호출을 진행합니다. 

res라는 변수를 이용해 dfs를 이용해 탐색한 경로의 길이까지 저장하는 함수를 구현해 봤습니다.

## BFS란?

너비 우선 탐색(Breadth-first search, BFS)는 맹목적 탐색 방법 중 하나로 시작 정점(vertex)을 방문한 후 인접한 모든 정점들을 우선으로 방문하는 방법입니다. 


더 이상 방문하지 않은 정점이 없을 때까지 방문하지 않은 정점들에 대해서도 너비 우선 탐색을 적용하고, 일반적으로 queue 자료 구조를 이용해서 순차적으로 접근이 가능하도록 구현이 가능합니다.
​

Tree 상에서 BFS로 탐색을 진행하는 경우에는 cycle이 생기는 경우가 없지만, graph에 BFS를 적용하는 경우에는 cycle이 있을 수 있기 때문에 무한 루프에 빠지는 것을 방지하기 위해서 방문 표시를 하면서 탐색을 진행해야 합니다.

## BFS 간단한 구현 방법

아래의 그림의 케이스를 예로 들겠습니다. '0' vertex에서 graph의 탐색을 시작한다고 가정하겠습니다. 그렇다면 '0'의 인접 vertex인 '1', '3' vertex를 방문하게 될 것입니다.

![image](https://postfiles.pstatic.net/MjAyMjA1MzFfOTUg/MDAxNjUzOTg2Nzc0MTU1.uiZNqkjB8IK9t83JThFqplq5GxeFkYjQw2VaTNTkzUgg.zq_PNdOb8VoDNEkUG0FyE91iZ4drN4VXQCC61BPZ1LUg.GIF.book541/graph_result.gif?type=w773)

이때, 인접한 vertex인 '1', '3'을 방문한 이후에는 다시 '1', '3'의 인접 vertex를 방문하게 될 텐데, 이때 이전에 방문한 vertex에 대한 방문 여부를 기록하지 않는다면, '3'의 인접한 vertex인 '0'을 다시 방문하고 '1'은 또 '3'과 다시 인접한 vertex이기 때문에 방문하게 되는 흐름에 빠져서 무한 루프를 돌게 될 것입니다.

따라서 방문한 vertex에 대한 방문 여부를 기록하면서 그래프 탐색을 진행해야 합니다.


또 '0' vertex에서 탐색을 시작해서 순차적으로 인접한 vertex를 방문하도록 구현하기 위해서 queue 자료 구조를 이용해야 합니다.

## Queue 자료 구조란?

![image](https://postfiles.pstatic.net/MjAyMjA1MzFfMzEg/MDAxNjUzOTg0ODgwNzE4.AKvOA6NslCnViXgbqaR8-GtMBvdd_yKK_1_MRnmXnnsg.B0v6RQi6QYYG9TGqbUwbcGfmdi4NhuZQTcJfIHtDC24g.GIF.book541/result_BFS.gif?type=w773)

큐(queue)는 컴퓨터 과학 분야에서 사용하는 기본적인 자료 구조의 한 종류로 FIFO(First in first out) 구조로 객체(데이터)를 저장하는 형식을 의미합니다.


큐 자료 구조는 DFS 구현에 사용하는 스택(stack)과 반대되는 개념으로 스택은 이전에도 보았듯이 나중에 넣은 데이터가 먼저 나오는 구조로 데이터를 관리합니다.


따라서 큐를 이용하면 방문하는 vertex의 인접한 verticies를 순서대로 방문하도록 구현할 수 있게 됩니다.

## BFS 예시 소스 코드 (with C++)

```c
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

int num = 7;
bool c[7];
vector<int> a[8];

void BFS(int start) {
	queue<int> q;
	q.push(start);
	c[start] = true;
	while (!q.empty()) {
		int x = q.front();
		q.pop();
		printf("%d ", x);
		for (int i = 0; i < a[x].size(); i++) {
			int y = a[x][i];
			if (!c[y]) {
				q.push(y);
				c[y] = true;
			}
		}
	}
}

int main() {
	a[0].push_back(3);
	a[0].push_back(1);

	a[1].push_back(3);
	a[1].push_back(2);
	a[1].push_back(4);

	a[2].push_back(4);

	a[3].push_back(0);
	// start from 1(start node)
	BFS(0);
	return 0;
}
```

- 예시 소스 코드 실행 결과

![image](https://postfiles.pstatic.net/MjAyMjA1MzFfMjg4/MDAxNjUzOTg2MTUwMzE2.0y0LM3oniK2eSOkkxB5UCj98bJFId9RkYtCMW--zuBUg.fGWx_oFHYfA4OaKljv7Yzaj_gsHQFwM9q9jTlJ2lzHYg.PNG.book541/image.png?type=w773)

위 소스 코드를 실행하면, 위와 같이 0, 3, 1, 2, 4 verticies를 순서대로 방문하는 결과를 확인할 수 있습니다.