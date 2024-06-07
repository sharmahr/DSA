[Prim's Algorithm](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

# Intuition
The problem requires finding the minimum spanning tree (MST) of a weighted undirected graph. The intuition is to use Prim's algorithm, which starts with an arbitrary vertex and greedily selects the minimum weight edge that connects a visited vertex to an unvisited vertex until all vertices are visited.

Note to remember: Prim's algorithm builds the MST by adding the minimum weight edge at each step, ensuring that the tree remains connected and has the minimum total weight.

# Approach
1. Create a priority queue `pq` to store vertices based on their weights. The priority queue will prioritize vertices with lower weights.

2. Initialize a boolean array `visited` to keep track of visited vertices.

3. Start the MST construction from vertex 0 by adding it to the priority queue with a weight of 0.

4. Initialize a variable `mstWeight` to store the total weight of the MST.

5. Iterate until all vertices are visited:
   - Extract the vertex `u` with the minimum weight from the priority queue.
   - If vertex `u` is already visited, continue to the next iteration.
   - Mark vertex `u` as visited.
   - Add the weight of the current edge to `mstWeight`.
   - Explore all adjacent vertices of vertex `u`:
     - For each adjacent vertex `v` with weight `w`:
       - If vertex `v` is not visited, add it to the priority queue with weight `w`.

6. Return the total weight of the MST stored in `mstWeight`.

# Complexity
- Time complexity:
  - The time complexity of Prim's algorithm using a priority queue is $O((V + E) \log V)$, where $V$ is the number of vertices and $E$ is the number of edges in the graph.
  - In the worst case, each vertex is added and removed from the priority queue once, resulting in $O(V \log V)$ operations. Additionally, each edge is processed once, resulting in $O(E \log V)$ operations.
* Space complexity:
  - The space complexity is $O(V)$ to store the `visited` array and the priority queue.

# Code
```java
class Solution {
    static int spanningTree(int V, int E, List<List<int[]>> adj) {
        // Create a priority queue to store vertices based on their weights
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
        
        // Initialize a boolean array to track visited vertices
        boolean[] visited = new boolean[V];
        
        // Start the MST construction from vertex 0
        pq.offer(new int[]{0, 0}); // {vertex, weight}
        
        // Initialize the total weight of the MST
        int mstWeight = 0;
        
        // Iterate until all vertices are visited
        while (!pq.isEmpty()) {
            // Extract the vertex with the minimum weight
            int[] curr = pq.poll();
            int u = curr[0];
            int weight = curr[1];
            
            // If the vertex is already visited, continue
            if (visited[u]) continue;
            
            // Mark the current vertex as visited
            visited[u] = true;
            
            // Add the weight of the current edge to the MST weight
            mstWeight += weight;
            
            // Explore all adjacent vertices of the current vertex
            for (int[] edge : adj.get(u)) {
                int v = edge[0];
                int w = edge[1];
                
                // If the adjacent vertex is not visited, add it to the priority queue
                if (!visited[v]) {
                    pq.offer(new int[]{v, w});
                }
            }
        }
        
        // Return the total weight of the MST
        return mstWeight;
    }
}
```