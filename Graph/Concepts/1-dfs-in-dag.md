[DFS Of Directed Acylic Graph](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

# Intuition
The problem requires performing a Depth-First Search (DFS) traversal on a given graph represented by an adjacency list. DFS explores as far as possible along each branch before backtracking, allowing us to visit all the vertices in a connected component of the graph.

# Approach
1. Create an ArrayList `list` to store the DFS traversal order of the vertices.
2. Create a boolean array `visited` to keep track of visited vertices.
3. Call the `dfsHelper` function with the adjacency list, starting vertex (0 in this case), `visited` array, and `list`.
4. In the `dfsHelper` function:
   - Check if the current vertex `u` is already visited. If so, return as it has been processed before.
   - Mark the current vertex `u` as visited.
   - Add the current vertex `u` to the `list`.
   - Iterate through all the adjacent vertices of `u` using the adjacency list `adj.get(u)`.
   - Recursively call `dfsHelper` for each unvisited adjacent vertex.
5. Return the `list` containing the DFS traversal order.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The DFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `visited` array and the recursion stack is proportional to the number of vertices.

# Code
```java
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        ArrayList<Integer> list = new ArrayList<>();
        boolean[] visited = new boolean[V];
        dfsHelper(adj, 0, visited, list);
        return list;
    }
    
    void dfsHelper(ArrayList<ArrayList<Integer>> adj, int u, boolean[] visited, ArrayList<Integer> list){
        if(visited[u]) return; // return as it is already visited
        
        visited[u] = true;
        list.add(u);
        for(int i:adj.get(u)){
            dfsHelper(adj, i, visited, list);
        }
    }
}
```