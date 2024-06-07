[Bipartite Graph using BFS](https://www.geeksforgeeks.org/problems/bipartite-graph/1)

# Intuition
To check if a graph is bipartite, we can use a two-coloring approach using breadth-first search (BFS). We start by assigning one color to a vertex and then alternately assign different colors to its adjacent vertices. If at any point we find that two adjacent vertices have the same color, it means the graph is not bipartite.

Note to remember: A graph is bipartite if it can be colored using two colors such that no two adjacent vertices have the same color.

# Approach
1. Create an integer array `color` of size `V` to store the color of each vertex. Initialize all elements to -1, indicating uncolored vertices.
2. Iterate through all the vertices from 0 to `V-1`.
   - If the current vertex `i` is uncolored (i.e., `color[i] == -1`), call the `bfsCheck` function to perform BFS starting from vertex `i`.
   - If the `bfsCheck` function returns `false` for any vertex, it means the graph is not bipartite, so return `false`.
3. If all vertices are successfully colored, return `true`.
4. In the `bfsCheck` function:
   - Create a queue and enqueue the starting vertex.
   - Assign color 0 to the starting vertex.
   - While the queue is not empty:
     - Dequeue a vertex `node` from the queue.
     - Get the current color of the vertex `node`.
     - Iterate through all the adjacent vertices of `node` using the adjacency list `adj.get(node)`.
       - If an adjacent vertex `neighbor` is uncolored (i.e., `color[neighbor] == -1`), assign the opposite color to it (i.e., `1 - currentColor`) and enqueue it.
       - If an adjacent vertex `neighbor` is already colored with the same color as `node`, it means the graph is not bipartite, so return `false`.
   - If all adjacent vertices are successfully colored, return `true`.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The BFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `color` array and the queue is proportional to the number of vertices.

# Code
```java
class Solution {
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>> adj) {
        int[] color = new int[V];
        Arrays.fill(color, -1); // Initialize all vertices as uncolored

        // BFS to check all components of the graph
        for (int i = 0; i < V; i++) {
            if (color[i] == -1) { // If the vertex is not colored
                if (!bfsCheck(adj, i, color)) {
                    return false;
                }
            }
        }
        
        return true;
    }

    private boolean bfsCheck(ArrayList<ArrayList<Integer>> adj, int start, int[] color) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start);
        color[start] = 0; // Start coloring with color 0
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            int currentColor = color[node];
            
            for (int neighbor : adj.get(node)) {
                if (color[neighbor] == -1) { // If the neighbor is not colored
                    color[neighbor] = 1 - currentColor; // Assign the opposite color
                    queue.offer(neighbor);
                } else if (color[neighbor] == currentColor) { // If the neighbor has the same color
                    return false;
                }
            }
        }
        
        return true;
    }
}
```