[Bipartite Graph using DFS](https://www.geeksforgeeks.org/problems/bipartite-graph/1)

# Intuition
To check if a graph is bipartite, we can assign colors (0 or 1) to each vertex such that no two adjacent vertices have the same color. If it is possible to color all the vertices in this way, then the graph is bipartite. We can use depth-first search (DFS) to traverse the graph and assign colors to the vertices.

Note to remember: A graph is bipartite if and only if it does not contain any odd-length cycles.

# Approach
1. Create an integer array `color` of size `V` to store the color of each vertex. Initialize all elements to -1, indicating uncolored vertices.
2. Iterate through all the vertices from 0 to `V-1`.
   - If the current vertex `i` is uncolored (i.e., `color[i] == -1`), call the `dfs` function to perform DFS starting from vertex `i` with color 0.
   - If the `dfs` function returns `false` for any vertex, it means the graph is not bipartite, so return `false`.
3. If all vertices are successfully colored, return `true`.
4. In the `dfs` function:
   - Assign the current color (`currentColor`) to the current vertex (`currentNode`).
   - Iterate through all the adjacent vertices of `currentNode` using the adjacency list `adj.get(currentNode)`.
     - If an adjacent vertex `i` is uncolored (i.e., `color[i] == -1`), recursively call `dfs` for vertex `i` with the opposite color (`1-currentColor`).
       - If the recursive call returns `false`, it means the graph is not bipartite, so return `false`.
     - If an adjacent vertex `i` is already colored with the same color as `currentNode`, it means the graph is not bipartite, so return `false`.
   - If all adjacent vertices are successfully colored, return `true`.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The DFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `color` array is proportional to the number of vertices.
  - The recursion stack can go up to a depth of `V` in the worst case.

# Code
```java
class Solution{
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>>adj)
    {
        // Code here
        int[] color = new int[V];
        Arrays.fill(color, -1);
        
        // green --> 0 and blue --> 1
        for(int i=0;i<V;i++){
            if(color[i] == -1){
                if(!dfs(adj, i, color, 0)) return false;
            }
        }
        
        return true;
    }
    
    public boolean dfs(ArrayList<ArrayList<Integer>> adj, int currentNode, int[] color, int currentColor){
        color[currentNode] = currentColor;
        for(int i:adj.get(currentNode)){
            if(color[i] == -1){
                if(!dfs(adj, i, color, 1-currentColor)) return false;
            }
            else if(color[i] == currentColor){
                return false;
            }
        }
        return true;
    }
}
```