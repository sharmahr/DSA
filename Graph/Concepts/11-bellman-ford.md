[Bellman Ford Algorithm](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1)

# Intuition
The Bellman-Ford algorithm is used to find the shortest paths from a single source vertex to all other vertices in a weighted graph, even if the graph contains negative edge weights. The algorithm works by relaxing edges repeatedly for V-1 iterations, where V is the number of vertices in the graph. After V-1 iterations, if there are still edges that can be relaxed, it indicates the presence of a negative cycle in the graph.

Note to remember: The Bellman-Ford algorithm can detect negative cycles in the graph, which is not possible with Dijkstra's algorithm.

# Approach
1. Initialize an array `dist` of size `V` to store the shortest distances from the source vertex `S` to all other vertices. Set all distances to a large value (e.g., 100000000) except for the source vertex, which has a distance of 0.

2. Relax edges V-1 times:
   - For each edge `(u, v)` with weight `weight` in the `edges` list:
     - If the distance to vertex `u` is not infinite and the distance to vertex `v` can be improved by taking the edge `(u, v)`, update the distance to vertex `v` as `dist[u] + weight`.

3. Check for negative cycles:
   - After V-1 iterations, if there are still edges that can be relaxed, it indicates the presence of a negative cycle.
   - For each edge `(u, v)` with weight `weight` in the `edges` list:
     - If the distance to vertex `u` is not infinite and the distance to vertex `v` can be improved by taking the edge `(u, v)`, return an array with a single element `-1` to indicate the presence of a negative cycle.

4. If no negative cycle is detected, return the `dist` array containing the shortest distances from the source vertex `S` to all other vertices.

# Complexity
- Time complexity:
  - The time complexity of the Bellman-Ford algorithm is $O(VE)$, where $V$ is the number of vertices and $E$ is the number of edges in the graph.
  - The outer loop runs for V-1 iterations, and the inner loop iterates over all the edges in each iteration.
* Space complexity:
  - The space complexity is $O(V)$ to store the `dist` array.

# Code
```java
class Solution {
    static int[] bellman_ford(int V, ArrayList<ArrayList<Integer>> edges, int S) {
        int[] dist = new int[V];
        Arrays.fill(dist, 100000000);
        dist[S] = 0;

        // Relax edges V-1 times
        for (int i = 0; i < V - 1; i++) {
            for (ArrayList<Integer> edge : edges) {
                int u = edge.get(0);
                int v = edge.get(1);
                int weight = edge.get(2);
                if (dist[u] != 100000000 && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                }
            }
        }

        // Check for negative cycle
        for (ArrayList<Integer> edge : edges) {
            int u = edge.get(0);
            int v = edge.get(1);
            int weight = edge.get(2);
            if (dist[u] != 100000000 && dist[u] + weight < dist[v]) {
                return new int[]{-1};
            }
        }

        return dist;
    }
}
```