# Important Graph Concepts to Understand

| Problem | Notes | Solution |
|:-------------|:--------------:|-------------:|
| [DFS Of Directed Acylic Graph](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1) | DFS explores as far as possible along each branch before backtracking, allowing us to visit all the vertices in a connected component of the graph. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/1-dfs-in-dag.md) |
| [BFS Of Directed Acylic Graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1) | BFS explores the graph level by level, visiting all the vertices at the current level before moving on to the next level. It uses a queue to keep track of the vertices to be visited. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/2-bfs-in-dag.md) |
| [Detect Cycle in Directed Graph using DFS](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1) |  Perform DFS traversal and keep track of the vertices that are currently being visited in the recursion stack (Separate Stack). If we encounter a vertex that is already in the recursion stack, it means we have found a cycle | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/3-detect-cycle-in-directed-graph.md) |
| [Topological Sort using DFS](https://www.geeksforgeeks.org/problems/topological-sort/1) | To find the topological ordering is by using depth-first search (DFS) and storing the vertices in a stack in the order of their completion times | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/4-topological-sort-dfs.md) |
| [Kahns Algorithm (Topological Sort using BFS)](https://www.geeksforgeeks.org/problems/topological-sort/1) | involves calculating the in-degree of each vertex and iteratively removing vertices with in-degree 0 and their outgoing edges | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/5-topological-sort-bfs.md) |
| [Bipartite Graph using DFS](https://www.geeksforgeeks.org/problems/bipartite-graph/1) | Use depth-first search (DFS) to traverse the graph and assign colors to the vertices. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/6-bipartite-graph-using-dfs.md) |
| [Bipartite Graph using BFS](https://www.geeksforgeeks.org/problems/bipartite-graph/1) | Start by assigning one color to a vertex and then alternately assign different colors to its adjacent vertices. If at any point we find that two adjacent vertices have the same color, it means the graph is not bipartite. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/7-bipartite-graph-using-bfs.md)|
| [Disjoint Set Union](https://www.geeksforgeeks.org/problems/disjoint-set-union-find/1) | The find operation determines the parent or representative of a set, while the union operation merges two sets together. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/8-disjoint-set-union.md) |
| [Disjoint Set Union by Path Compression](https://www.geeksforgeeks.org/problems/disjoint-set-union-find/1) | The find operation determines the parent or representative of a set, while the union operation merges two sets together based on their ranks. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/9-disjoint-set-union-by-rank-path-compression.md) |
| [Dijkstras Algorithm](https://www.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1) | Maintain a priority queue of vertices based on their tentative distances from the source vertex. At each step, the vertex with the minimum tentative distance is selected, and its adjacent vertices are updated if a shorter path is found. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/10-dijkstras-alogrithm.md) |
| [Bellman Ford Algorithm](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1) | The Bellman-Ford algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even if the graph contains negative edge weights. The algorithm works by relaxing edges repeatedly for V-1 iterations, where V is the number of vertices in the graph. After V-1 iterations, if there are still edges that can be relaxed, it indicates the presence of a negative cycle in the graph. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/11-bellman-ford.md) |
| [Flyod Warshal Algorithm](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1) | The Floyd-Warshall algorithm is used to find the shortest distances between all pairs of vertices in a weighted graph. The algorithm works by considering all vertices as potential intermediate vertices and incrementally updating the shortest distances between pairs of vertices. It can handle negative edge weights but not negative cycles. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/12-floyd-warshal.md) |
| [Prims Algorithm](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1) | Start with an arbitrary vertex and greedily selects the minimum weight edge that connects a visited vertex to an unvisited vertex until all vertices are visited. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/13-prims-algorithm.md) |
| [Kruskal's Algorithm](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1) | Start by sorting all the edges in ascending order of their weights and then greedily selects the minimum weight edge that does not create a cycle until all vertices are connected. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/14-kruskals-algorithm.md) |
| [Kosaraju's Algorithm](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1) | Perform two depth-first search (DFS) traversals on the graph. The first DFS helps in finding the order of vertices based on their completion times, and the second DFS on the transposed graph helps in identifying the SCCs. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/15-kosarajus-algorithm.md) |
| [Euler Circuit and Path](https://www.geeksforgeeks.org/problems/euler-circuit-and-path/1) | To determine if a graph contains an Eulerian circuit or an Eulerian path, we can use the following properties:An Eulerian circuit exists if all vertices have an even degree.An Eulerian path exists if exactly two vertices have an odd degree. | [Solution](https://github.com/sharmahr/DSA/blob/main/Graph/Concepts/16-euler-circuit-and-path.md) |



## Identifying Graph Problems:

Graph problems often involve relationships between entities. Look for these indicators:
1. Connections or relationships between objects
2. Networks (social, computer, transportation)
3. Dependencies or hierarchies
4. Paths or routes between points
5. Optimization problems involving connections

Now, let's discuss when to use each concept:

1. Depth-First Search (DFS):
   Use when:
   - You need to explore as far as possible along each branch before backtracking
   - Solving maze-like puzzles
   - Finding connected components
   - Detecting cycles in a graph
   - Topological sorting

   Example: Finding a path in a maze

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    for next in graph[start] - visited:
        dfs(graph, next, visited)
    return visited
```

2. Breadth-First Search (BFS):
   Use when:
   - You need to find the shortest path on unweighted graphs
   - Exploring neighbors before going to next level
   - Level-order traversal
   - Finding connected components

   Example: Finding shortest path in an unweighted graph

```python
from collections import deque

def bfs(graph, start):
    visited, queue = set(), deque([start])
    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            visited.add(vertex)
            queue.extend(graph[vertex] - visited)
    return visited
```

3. Topological Sort:
   Use when:
   - You have a directed acyclic graph (DAG) and need to order tasks with dependencies
   - Scheduling problems
   - Build systems

   Example: Course schedule problem

```python
def topological_sort(graph):
    visited = set()
    stack = []
    
    def dfs(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs(neighbor)
        stack.append(node)
    
    for node in graph:
        if node not in visited:
            dfs(node)
    
    return stack[::-1]
```

4. Kahn's Algorithm:
   Use when:
   - You need a topological sort but prefer an iterative approach
   - You want to detect cycles in a directed graph

   Example: Finding order of tasks

```python
from collections import deque

def kahns_algorithm(graph):
    in_degree = {node: 0 for node in graph}
    for node in graph:
        for neighbor in graph[node]:
            in_degree[neighbor] += 1
    
    queue = deque([node for node in graph if in_degree[node] == 0])
    result = []
    
    while queue:
        node = queue.popleft()
        result.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    if len(result) != len(graph):
        return None  # Graph has a cycle
    return result
```

5. Bipartite Graphs:
   Use when:
   - You need to divide a set of objects into two groups with no connections within the same group
   - Matching problems (e.g., job assignments)

   Example: Checking if a graph is bipartite

```python
def is_bipartite(graph):
    color = {}
    def dfs(node):
        for neighbor in graph[node]:
            if neighbor in color:
                if color[neighbor] == color[node]:
                    return False
            else:
                color[neighbor] = 1 - color[node]
                if not dfs(neighbor):
                    return False
        return True
    
    for node in graph:
        if node not in color:
            color[node] = 0
            if not dfs(node):
                return False
    return True
```

6. Disjoint Set (Union-Find):
   Use when:
   - You need to keep track of a partition of a set of elements
   - Finding connected components
   - Cycle detection in undirected graphs

   Example: Implementing disjoint set

```python
class DisjointSet:
    def __init__(self, vertices):
        self.parent = {v: v for v in vertices}
        self.rank = {v: 0 for v in vertices}
    
    def find(self, item):
        if self.parent[item] != item:
            self.parent[item] = self.find(self.parent[item])
        return self.parent[item]
    
    def union(self, x, y):
        xroot, yroot = self.find(x), self.find(y)
        if self.rank[xroot] < self.rank[yroot]:
            self.parent[xroot] = yroot
        elif self.rank[xroot] > self.rank[yroot]:
            self.parent[yroot] = xroot
        else:
            self.parent[yroot] = xroot
            self.rank[xroot] += 1
```

7. Dijkstra's Algorithm:
   Use when:
   - You need to find the shortest path in a weighted graph with non-negative edges
   - Routing problems

   Example: Finding shortest path

```python
import heapq

def dijkstra(graph, start):
    distances = {node: float('infinity') for node in graph}
    distances[start] = 0
    pq = [(0, start)]
    
    while pq:
        current_distance, current_node = heapq.heappop(pq)
        if current_distance > distances[current_node]:
            continue
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))
    
    return distances
```

8. Bellman-Ford Algorithm:
   Use when:
   - You need to find the shortest path in a weighted graph that may contain negative edges
   - Detecting negative cycles

   Example: Finding shortest path with possible negative edges

```python
def bellman_ford(graph, start):
    distances = {node: float('infinity') for node in graph}
    distances[start] = 0
    
    for _ in range(len(graph) - 1):
        for node in graph:
            for neighbor, weight in graph[node].items():
                if distances[node] + weight < distances[neighbor]:
                    distances[neighbor] = distances[node] + weight
    
    # Check for negative cycles
    for node in graph:
        for neighbor, weight in graph[node].items():
            if distances[node] + weight < distances[neighbor]:
                return None  # Negative cycle detected
    
    return distances
```

9. Floyd-Warshall Algorithm:
   Use when:
   - You need to find the shortest paths between all pairs of vertices
   - The graph is dense

   Example: All-pairs shortest path

```python
def floyd_warshall(graph):
    distances = {node: {node: float('infinity') for node in graph} for node in graph}
    for node in graph:
        distances[node][node] = 0
        for neighbor, weight in graph[node].items():
            distances[node][neighbor] = weight
    
    for k in graph:
        for i in graph:
            for j in graph:
                distances[i][j] = min(distances[i][j], distances[i][k] + distances[k][j])
    
    return distances
```

10. Prim's Algorithm:
    Use when:
    - You need to find a minimum spanning tree in a weighted, undirected graph
    - The graph is dense

    Example: Finding minimum spanning tree

```python
import heapq

def prims(graph):
    start_node = next(iter(graph))
    mst = []
    visited = set([start_node])
    edges = [(cost, start_node, to) for to, cost in graph[start_node].items()]
    heapq.heapify(edges)
    
    while edges:
        cost, frm, to = heapq.heappop(edges)
        if to not in visited:
            visited.add(to)
            mst.append((frm, to, cost))
            for next_node, next_cost in graph[to].items():
                if next_node not in visited:
                    heapq.heappush(edges, (next_cost, to, next_node))
    
    return mst
```

11. Kruskal's Algorithm:
    Use when:
    - You need to find a minimum spanning tree in a weighted, undirected graph
    - The graph is sparse

    Example: Finding minimum spanning tree

```python
def kruskals(graph):
    edges = [(cost, u, v) for u in graph for v, cost in graph[u].items()]
    edges.sort()
    
    disjoint_set = DisjointSet(graph.keys())
    mst = []
    
    for cost, u, v in edges:
        if disjoint_set.find(u) != disjoint_set.find(v):
            disjoint_set.union(u, v)
            mst.append((u, v, cost))
    
    return mst
```

Building Intuition:
- Use DFS for exploring all possibilities or finding cycles
- Use BFS for shortest path in unweighted graphs or level-order traversal
- Use Topological Sort or Kahn's for dependency ordering
- Use Bipartite for two-color problems or matching
- Use Disjoint Set for grouping elements or finding cycles in undirected graphs
- Use Dijkstra's for shortest path with non-negative weights
- Use Bellman-Ford for shortest path with possible negative weights
- Use Floyd-Warshall for all-pairs shortest path in dense graphs
- Use Prim's or Kruskal's for minimum spanning trees
