> 나동빈님의 서적 ['이것이 취업을 위한 코딩테스트다'](https://play.google.com/store/books/details/%EB%82%98%EB%8F%99%EB%B9%88_%EC%9D%B4%EA%B2%83%EC%9D%B4_%EC%B7%A8%EC%97%85%EC%9D%84_%EC%9C%84%ED%95%9C_%EC%BD%94%EB%94%A9_%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4_with_%ED%8C%8C%EC%9D%B4%EC%8D%AC?id=vBz-DwAAQBAJ)를 읽고 정리하였습니다.



## 플로이드 워셜(Floyd-Warshall) 알고리즘

다익스트라 알고리즘은 '한 지점에서 다른 특정 지점까지 최단 경로를 구해야 하는 경우'에 사용할 수 있는 최단 경로 알고리즘이었다.

플로이드 워셜 알고리즘은 '모든 지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우'에 사용할 수 있는 알고리즘이다.



## 핵심 아이디어

다익스트라 알고리즘은 단계마다 최단 거리를 가지는 노드를 하나씩 반복적으로 선택한다. 그리고 해당 노드를 거쳐 가는 경로를 확인하며, 최단 거리 테이블을 갱신하는 방식으로 동작한다.

플로이드 워셜 알고리즘 또한 단계마다 거쳐 가는 노드를 기준으로 알고리즘을 수행한다. 하지만 매번 방문하지 않은 노드 중에서 최단 거리를 갖는 노드를 찾을 필요가 없다는 점이 다르다.



## 시간 복잡도

노드의 개수가 N개일 때 알고리즘상으로 O(N^2)연산을 N번 수행하여 '현재 노드를 거쳐가는' 모든 경로를 고려한다. 따라서 플로이드 워셜 알고리즘의 총 시간 복잡도는 O(N^3)이다.

다익스트라 알고리즘에서는 출발 노드가 1개이므로 다르 모든 노드까지의 최단 거리를 저장하기 위해 1차원 리스트를 이용했다.

반면에 플로이드 워셜 알고리즘은 2차원 리스트에 '최단 거리' 정보를 저장한다. 모든 노드에 대하여 다르 모든 노드로 가는 최단 거리 정보를 담아야 하기 때문이다. 그래서 N번의 단계에서 매번 O(N^2)의 시간이 소요된다.



### 구현

#### 방법 

- 플로이드 워셜 알고리즘은 다이나믹 프로그래밍
  - 다익스트라 알고리즘은 그리드 알고리즘
- 노드의 개수가 N일 때, N번 만큼의 단계를 반복하며 '점화식에 맞게' 2차원 리스트를 갱신한다.
- 각 단계에서는 해당 노드(k)를 거쳐 가는 경우를 고려한다. 점화식은 아래와 같다.

<img src="https://user-images.githubusercontent.com/71204049/141919654-2ebae6d9-5533-41f8-8935-6c89e9b26ea4.png" width="200" />



#### 코드

```python
import sys

# 무한을 의미하는 값으로 10억을 설정
INF = int(1e9)

# 노드의 개수 및 간선의 개수를 입력받는다.
n = int(sys.stdin.readline().strip())
m = int(sys.stdin.readline().strip())
# 2차원 리스트를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 본인 -> 본인 경로 비용은 0으로 초기화
for i in range(1, n + 1):
    graph[i][i] = 0

# 각 간선에 대한 정보를 입력받아 그 값으로 초기화
for _ in range(m):
    # a -> b 비용은 c
    a, b, c = map(int, sys.stdin.readline().strip().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])


```
