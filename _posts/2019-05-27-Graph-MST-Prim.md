# Prim의 MST 알고리즘

> + 시작 정점에서부터 출발하여 신장 트리 집합을 단계적으로 확장해 나가는 방법
> + 앞 단계에서 만들어진 신장 트리 집합에 인접한 정점들 중에서 최소 간선으로 연결된 정점을 선택하여 트리를 확장
> + 이 과정은 트리가 n-1개의 간선을 가질 때까지 계속


| Kruscal | Prim |
| --------|----------- |
| 간선 선택을 기반 | 정점 선택을 기반 |
| 이전 단계와 상관없이 무조건 최선 간선 선택 | 이전 단계에서 만들어진 신장트리를 확장 |
| O(elog<sub>2</sub>e) | O(n<sup>2</sup>) |


~~~cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <limits.h>

#define MAX_VERTICES	7
#define INF		(INT_MAX / 2)

int weight[MAX_VERTICES][MAX_VERTICES] = {
        { 0, 29, INF, INF, INF, 10, INF },
        { 29, 0, 16, INF, INF, INF, 15  },
        { INF, 16, 0, 12, INF, INF, INF },
        { INF, INF, 12, 0, 22, INF, 18  },
        { INF, INF, INF, 22, 0, 27, 25  },
        { 10, INF, INF, INF, 27, 0, INF },
        { INF, 15, INF, 18, 25, INF , 0 }
};

bool selected[MAX_VERTICES];
int dist[MAX_VERTICES];

int get_min_vertex(int n)
{
	int i, c;

	for (i = 0; i < n; i++) {
		if (selected[i] == false) {
			c = i;
		}
	}

	for (i = 0; i < n; i++) {
		if (selected[i] == false && dist[c] > dist[i])
			c = i;
	}

	return c;
}

void prim(int n, int s)
{
	int i, u, v;

	for (i = 0; i < n; i++) {
		dist[i] = INF;
		selected[i] = false;
	}

	dist[s] = 0;

	for (i = 0; i < n; i++) {
		u = get_min_vertex(n);
		selected[u] = true;

		if (dist[u] == INF) return;

		printf("%d  ", u);

		for (v = 0; v < n; v++) {
			if (weight[u][v] != INF) {
				if (!selected[v] && (weight[u][v] < dist[v]))
					dist[v] = weight[u][v];
			}
		}
	}

	printf("\n");
}

int main(void)
{
	prim(MAX_VERTICES, 0);

	return 0;
}

~~~
