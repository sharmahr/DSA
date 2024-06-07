[Detect Cycle in Directed Graph using DFS](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)

# Intuition
To detect a cycle in a directed graph, we can perform a depth-first search (DFS) traversal and keep track of the vertices that are currently being visited in the recursion stack. If we encounter a vertex that is already in the recursion stack, it means we have found a cycle.

# Approach
1. Create two boolean arrays: `visited` and `inRecursion`, both of size `V` (number of vertices).
   - `visited[i]` indicates whether vertex `i` has been visited during the DFS traversal.
   - `inRecursion[i]` indicates whether vertex `i` is currently in the recursion stack.
2. Iterate through all the vertices from 0 to `V-1`.
   - If vertex `i` is not visited, call the `isCyclicHelper` function to check for a cycle starting from vertex `i`.
   - If the `isCyclicHelper` function returns `true`, it means a cycle is found, so return `true`.
3. If no cycle is found after checking all the vertices, return `false`.
4. In the `isCyclicHelper` function:
   - Mark the current vertex `u` as visited and in the recursion stack.
   - Iterate through all the adjacent vertices of `u` using the adjacency list `adj.get(u)`.
     - If an adjacent vertex `i` is not visited, recursively call `isCyclicHelper` for vertex `i`.
       - If the recursive call returns `true`, it means a cycle is found, so return `true`.
     - If an adjacent vertex `i` is already in the recursion stack, it means a cycle is found, so return `true`.
   - Mark the current vertex `u` as not in the recursion stack anymore.
   - If no cycle is found, return `false`.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The DFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `visited` and `inRecursion` arrays is proportional to the number of vertices.
  - The recursion stack can go up to a depth of `V` in the worst case.

# Code
```java
class Solution {
    // Function to detect cycle in a directed graph.
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        // code here
        boolean[] visited = new boolean[V];
        boolean[] inRecursion = new boolean[V];
        for(int i=0;i<V;i++){
            if(!visited[i] && isCyclicHelper(adj, i, visited, inRecursion)) return true;
        }
        return false;
    }
    
    public boolean isCyclicHelper(ArrayList<ArrayList<Integer>> adj, int u, boolean[] visited, boolean[] inRecursion){
        visited[u] = true;
        inRecursion[u] = true;
        for(int i:adj.get(u)){
            // if not visited, then we check for cycle in dfs
            if(!visited[i] && isCyclicHelper(adj, i, visited, inRecursion)){
                return true;
            }else if(inRecursion[i]){
                return true;
            }
        }
        inRecursion[u] = false;
        return false;
    }
}
```