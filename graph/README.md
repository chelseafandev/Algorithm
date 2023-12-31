## graph

**목차**
- [graph](#graph)
  - [adjacency matrix(인접 행렬)](#adjacency-matrix인접-행렬)
  - [adjacency list(인접 리스트)](#adjacency-list인접-리스트)
  - [4방향 탐색과 direction vector](#4방향-탐색과-direction-vector)
  - [dfs(depth first search) --- stack](#dfsdepth-first-search-----stack)
  - [bfs(breadth first search) --- queue](#bfsbreadth-first-search-----queue)
  - [tree travesal](#tree-travesal)
  - [dijkstra(최단 경로 탐색 알고리즘)](#dijkstra최단-경로-탐색-알고리즘)

<br>
<br>

### adjacency matrix(인접 행렬)
인접 행렬이란 그래프에서 정점과 간선의 관계를 나타내는 bool 타입의 정사각형 행렬을 의미하며 정사각형 행렬의 각 요소는 0 또는 1이라는 값을 갖습니다. 0은 두 정점 사이의 경로가 없음을 의미하며 1은 두 정점 사이의 경로가 있음을 의미합니다.

<br>

*reference*
- https://blog.naver.com/jhc9639/222289089015A  

<br>

### adjacency list(인접 리스트)
인접 리스트는 그래프에서 정점과 간선의 관계를 나타내는 연결리스트를 의미하며, list가 아닌 vector로 구현해도 무방합니다. 정점 별로 벡터를 생성하여 해당 정점에 인접한 정점들을 벡터의 요소로 추가합니다.

*reference*
- https://blog.naver.com/jhc9639/222289089015

<br>

### 4방향 탐색과 direction vector
```cpp
const int dy[] = {-1, 0, 1, 0};
const int dx[] = {0, 1, 0, -1};
for(int i = 0; i < 4; i++){
    ny = y + dy[i];
    nx = x + dx[i];
}
```

### dfs(depth first search) --- stack
DFS는 그래프를 탐색할 때 쓰는 알고리즘이며 어떤 노드부터 시작해 인접한 노드들을 재귀적으로 방문하며 방문한 정점은 다시 방문하지 않으며 각 분기마다 가능한 가장 멀리 있는 노드까지 탐색하는 알고리즘입니다.

그래프에서 깊이 우선 탐색은 트리의 깊이 우선 탐색과 유사합니다. 트리와의 차이점은 그래프는 (특정 노드를 2번 방문할 수도 있는)순환을 포함할 수 있다는 점입니다. 동일한 노드를 한번 더 처리하는 것을 피하기 위해서 방문 여부를 bool값 형태로 저장하는 배열을 사용합니다.
> Depth First Traversal (or Search) for a graph is similar to Depth First Traversal of a tree. The only catch here is, unlike trees, graphs may contain cycles (a node may be visited twice). To avoid processing a node more than once, use a boolean visited array.

Example:
```diff
Input: n = 4, e = 6
0 -> 1, 0 -> 2, 1 -> 2, 2 -> 0, 2 -> 3, 3 -> 3
Output: DFS from vertex 1 : 1 2 0 3
```
![](../resources/images/dfs-figure-1.jpg)

```diff
Input: n = 4, e = 6
2 -> 0, 0 -> 2, 1 -> 2, 0 -> 1, 3 -> 3, 1 -> 3
Output: DFS from vertex 2 : 2 0 1 3
```
![](../resources/images/dfs-figure-2.png)

<br>

*reference*
- https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/
- https://blog.naver.com/jhc9639/222289089015

<br>

### bfs(breadth first search) --- queue
BFS는 그래프를 탐색하는 알고리즘이며 어떤 정점에서 시작해 다음 깊이의 정점으로 이동하기전 현재 깊이의 모든 정점을 탐색하며 방문한 정점은 다시 방문하지 않는 알고리즘입니다. ***같은 가중치를 가진 그래프에서 최단거리알고리즘***으로 쓰입니다.

그래프에서 너비 우선 탐색은 트리의 너비 우선 탐색과 유사합니다. 트리와의 차이점은 그래프는 순환을 포함할 수 있다는 점입니다. 그래서 우리는 동일한 노드로 다시 돌아 올 수도 있습니다. 동일한 노드를 한번 더 처리하는 것을 피하기 위해서 방문 여부를 bool값 형태로 저장하는 배열을 사용합니다. 문제를 단순화하기 위해 모든 vertex들은 시작 지점으로부터 도달 가능하다고 가정하겠습니다.
> Breadth-First Traversal (or Search) for a graph is similar to Breadth-First Traversal of a tree. The only catch here is, unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array. For simplicity, it is assumed that all vertices are reachable from the starting vertex.

예를 들어, 아래 그래프는 2번 vertex에서 탐색을 시작합니다. 0번 vertex에 도달했을때 해당 vertex에 인접한 모든 vertex들을 찾습니다. 시작 지점이었던 2번 vertex 또한 0번 vertex에 인접해있습니다. 만약 방문했던 vertex를 표시하지 않는다면 2번 vertex는 다시 한번 처리될 것이고 절대 종료되지 않는 프로세스가 되어버릴 것입니다. 아래 그래프의 너비 우선 탐색 결과는 2, 0, 3, 1 입니다.
> For example, in the following graph, we start traversal from vertex 2. When we come to vertex 0, we look for all adjacent vertices of it. 2 is also an adjacent vertex of 0. If we don’t mark visited vertices, then 2 will be processed again and it will become a non-terminating process. A Breadth-First Traversal of the following graph is 2, 0, 3, 1.

![](../resources/images/bfs-figure-1.png)

<br>

*reference*
- https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
- https://blog.naver.com/jhc9639/222289089015

<br>

### tree travesal
후위순회(postorder traversal): 자식 노드를 방문하고 자신의 노드를 방문하는 것을 말합니다.
전위순회(preorder traversal): 먼저 자신의 노드를 방문하고 그 다음 자식 노드들을 방문하는 것을 말합니다.
중위순회(inorder traversal): 왼쪽 노드를 먼저 방문 그 다음 자신의 노드를 방문하고 그 다음 오른쪽 노드를 방문하는 것을 말합니다.
레벨순회(level traversal): BFS를 생각하면 됩니다.

<br>

### dijkstra(최단 경로 탐색 알고리즘)
그래프와 그래프의 출발 정점가 주어지는 경우에 출발 정점에서 주어진 그래프의 모든 정점까지의 최단 경로를 찾아보겠습니다. 다익스트라 알고리즘은 최소 신장 트리(minimum spanning tree)에 대한 Prim 알고리즘과 매우 유사합니다. Prim의 MST와 마찬가지로 주어진 출발 정점을 루트로 사용하여 SPT(최단 경로 트리)를 생성합니다.
> Given a graph and a source vertex in the graph, find the shortest paths from the source to all vertices in the given graph. Dijkstra’s algorithm is very similar to Prim’s algorithm for minimum spanning tree. Like Prim’s MST, we generate a SPT (shortest path tree) with a given source as a root.

우리는 2가지 set을 유지하게 되는데 하나는 최단 경로 트리에 포함된 정점들을 저장하는 set이고 다른 하나는 아직 최단 경로 트리에 포함되지 않은 정점들을 저장하는 set입니다. 알고리즘의 매 스텝마다 최단 경로 트리에 아직 포함되지 않았으며 출발지로부터 거리가 최소인 정점를 찾게 됩니다.
> We maintain two sets, one set contains vertices included in the shortest-path tree, other set includes vertices not yet included in the shortest-path tree. At every step of the algorithm, we find a vertex that is in the other set (set of not yet included) and has a minimum distance from the source.

아래 과정은 주어진 그래프에서 단일 출발 정점로부터 다른 모든 정점들까지의 최단 경로를 찾는 다익스트라 알고리즘의 세부적인 내용입니다.
> Below are the detailed steps used in Dijkstra’s algorithm to find the shortest path from a single source vertex to all other vertices in the given graph.

1) 최단 경로 트리안에 포함된 정점들을 트랙킹하는 set(sptSet)을 생성합니다. 최초 이 set은 비어있습니다.
2) 주어진 그래프의 모든 정점들에 거리 값을 할당해줍니다. 모든 거리 값을 INFINITE로 초기화합니다. 가장 먼저 선택되는 출발지 정점의 거리 값은 0으로 할당합니다.
3) sptSet이 모든 정점들을 포함하지 않는 동안
   - 최소 거리 값을 가지며 sptSet에 포함되어있지 않은 정점 u를 선택합니다.
   - 정점 u를 sptSet에 포함시킵니다.
   - 정점 u에 인접해있는 모든 정점들의 거리 값을 업데이트 합니다. 거리 값을 업데이트하기 위해 인접한 모든 정점들을 순회합니다. 모든 인접한 정점 v에 대해서 정점 u에서 v까지의 엣지의 가중치와 출발지로부터 정점 u까지의 거리합이 정점 v의 거리 값보다 작은 경우라면 정점 v의 거리 값을 업데이트 해줍니다.
> 1) Create a set sptSet (shortest path tree set) that keeps track of vertices included in the shortest-path tree, i.e., whose minimum distance from the source is calculated and finalized. Initially, this set is empty.
> 2) Assign a distance value to all vertices in the input graph. Initialize all distance values as INFINITE. Assign distance value as 0 for the source vertex so that it is picked first.
> 3) While sptSet doesn’t include all vertices
> …a) Pick a vertex u which is not there in sptSet and has a minimum distance value.
> …b) Include u to sptSet.
> …c) Update distance value of all adjacent vertices of u. To update the distance values, iterate through all adjacent vertices. For every adjacent vertex v, if the sum of distance value of u (from source) and weight of edge u-v, is less than the distance value of v, then update the distance value of v.

아래 예제를 통해 이해해보도록 하겠습니다.
> Let us understand with the following example:
![](../resources/images/dijkstra-figure1.jpg)

sptSet은 최초 비어있는 상태이며 정점들에 할당된 거리 값은 {0, INF, INF, INF, INF, INF, INF, INF} 입니다. 이제 가장 작은 거리 값을 갖는 정점를 선택합니다. 정점 0이 선택되며 정점 0을 sptSet 안에 포함시킵니다. 그렇게되면 sptSet은 {0}이 될 것입니다. sptSet에 정점 0를 포함시킨 후에 정점 0에 인접한 정점들의 거리 값을 업데이트합니다. 정점 0에 인접한 정점들은 정점 1과 7입니다. 정점 1과 7의 거리 값은 4와 8로 각각 업데이트 됩니다. 아래 서브그래프에서 정점들과 그것들의 거리 값을 보여주고 있으며 오직 유한한 거리를 갖는 정점들만 보여집니다. 최단 경로 트리(SPT)에 포함된 정점들은 초록색으로 표시됩니다.
> The set sptSet is initially empty and distances assigned to vertices are {0, INF, INF, INF, INF, INF, INF, INF} where INF indicates infinite. Now pick the vertex with a minimum distance value. The vertex 0 is picked, include it in sptSet. So sptSet becomes {0}. After including 0 to sptSet, update distance values of its adjacent vertices. Adjacent vertices of 0 are 1 and 7. The distance values of 1 and 7 are updated as 4 and 8. The following subgraph shows vertices and their distance values, only the vertices with finite distance values are shown. The vertices included in SPT are shown in green colour.

![](../resources/images/dijkstra-figure2.jpg)

아직 최단 경로 트리에 포함되지 않았으며(sptSet에 포함되지 않은) 최소 거리 값을 갖는 정점를 선택합니다. 정점 1이 선택되고 sptSet에 추가됩니다. sptSet은 이제 {0, 1}이 됩니다. 정점 1에 인접한 정점들의 거리 값을 업데이트 해줍니다. 정점 2의 거리 값은 12가 됩니다. (정점 7도 인접해있지만 거리 값이 8로 설정되어있으며 이는 출발지인 정점 0에서 정점 1까지의 거리인 4와 정점 4에서 정점 8까지의 거리 값인 11의 합인 15보다 작기때문에 갱신하지 않음)
> Pick the vertex with minimum distance value and not already included in SPT (not in sptSET). The vertex 1 is picked and added to sptSet. So sptSet now becomes {0, 1}. Update the distance values of adjacent vertices of 1. The distance value of vertex 2 becomes 12.

![](../resources/images/dijkstra-figure3.jpg)

아직 최단 경로 트리에 포함되지 않았으며(sptSet에 포함되지 않은) 최소 거리 값을 갖는 정점를 선택합니다. 정점 7이 선택됩니다. sptSet은 {0, 1, 7}이 됩니다. 정점 7에 인접한 정점들의 거리 값을 업데이트 해줍니다. 정점 6과 8의 거리 값은 각각 15와 9가 됩니다.
> Pick the vertex with minimum distance value and not already included in SPT (not in sptSET). Vertex 7 is picked. So sptSet now becomes {0, 1, 7}. Update the distance values of adjacent vertices of 7. The distance value of vertex 6 and 8 becomes finite (15 and 9 respectively). 

![](../resources/images/dijkstra-figure4.jpg)

아직 최단 경로 트리에 포함되지 않았으며(sptSet에 포함되지 않은) 최소 거리 값을 갖는 정점를 선택합니다. 정점 6이 선택됩니다. sptSet은 {0, 1, 7, 6}이 됩니다. 정점 6에 인접한 정점들의 거리 값을 업데이트 해줍니다. 정점 5와 8의 거리 값을 업데이트 해줍니다. (여기서 정점 8의 경우에는 해당 정점의 거리 값이 15이고 출발지인 정점 0에서 정점 6까지의 거리인 9와 정점 6에서 정점 8까지의 거리 깂인 6의 합인 15와 같기때문에 굳이 갱신할 필요는 없음)
> Pick the vertex with minimum distance value and not already included in SPT (not in sptSET). Vertex 6 is picked. So sptSet now becomes {0, 1, 7, 6}. Update the distance values of adjacent vertices of 6. The distance value of vertex 5 and 8 are updated.

![](../resources/images/dijkstra-figure5.jpg)

위 과정들을 sptSet에 주어진 그래프의 모든 노드가 포함될때까지 반복합니다. 최종적으로 아래와 같은 최단 경로 트리를 얻어내게 됩니다.
> We repeat the above steps until sptSet includes all vertices of the given graph. Finally, we get the following Shortest Path Tree (SPT).
![](../resources/images/dijkstra-figure6.jpg)

<br>

*reference*
- https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/