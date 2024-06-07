[Dijkstras Algorithm](https://www.geeksforgeeks.org/problems/implementing-dijkstra-set-1-adjacency-matrix/1)

# Intuition
The problem requires finding the shortest distance from a source vertex to all other vertices in a weighted graph. Dijkstra's algorithm is a well-known algorithm for solving this problem. The intuition behind Dijkstra's algorithm is to maintain a priority queue of vertices based on their tentative distances from the source vertex. At each step, the vertex with the minimum tentative distance is selected, and its adjacent vertices are updated if a shorter path is found.

Note to remember: Dijkstra's algorithm works for graphs with non-negative edge weights and finds the shortest path from a single source vertex to all other vertices.

# Approach
1. Initialize an array `dist` of size `V` to store the shortest distances from the source vertex `S` to all other vertices. Set all distances to a large value (e.g., `Integer.MAX_VALUE`) except for the source vertex, which has a distance of 0.

2. Create a priority queue `pq` to store vertices along with their tentative distances. The priority queue is implemented as a min-heap based on the tentative distances.

3. Add the source vertex `S` to the priority queue with a distance of 0.

4. While the priority queue is not empty, repeat the following steps:
   - Remove the vertex `u` with the minimum tentative distance from the priority queue.
   - If the tentative distance of `u` is greater than the current shortest distance stored in `dist[u]`, skip this vertex and continue to the next iteration.
   - For each adjacent vertex `v` of `u`:
     - Calculate the tentative distance to `v` through `u` by adding the weight of the edge `(u, v)` to the shortest distance of `u`.
     - If the tentative distance is smaller than the current shortest distance stored in `dist[v]`, update `dist[v]` with the tentative distance and add `v` to the priority queue with the updated distance.

5. After the priority queue is empty, the `dist` array will contain the shortest distances from the source vertex `S` to all other vertices.

# Complexity
- Time complexity:
  - The time complexity of Dijkstra's algorithm using a priority queue is $O((V + E) \log V)$, where $V$ is the number of vertices and $E$ is the number of edges in the graph.
  - In the worst case, each vertex is added and removed from the priority queue once, resulting in $O(V \log V)$ operations. Additionally, each edge is processed once, resulting in $O(E \log V)$ operations.
* Space complexity:
  - The space complexity is $O(V)$ to store the `dist` array and the priority queue.

# Code
```java
class Solution {
    //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[S] = 0;

        // min heap
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]); // refer for the syntax explanation

        // pq.offer(new int[]{S, 0}) adds a new element to the priority queue pq.
        // new int[]{S, 0} --> creates a new integer array with two elements
        pq.offer(new int[]{S, 0});

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int u = curr[0];
            int w = curr[1];

            if (w > dist[u]) {
                continue;
            }

            for (ArrayList<Integer> edge : adj.get(u)) {
                int v = edge.get(0);
                int weight = edge.get(1);

                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.offer(new int[]{v, dist[v]});
                }
            }
        }
        return dist;
    }
}
```