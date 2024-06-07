[Kosaraju's Algorithm](https://www.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1)

# Intuition
The problem requires finding the number of strongly connected components (SCCs) in a directed graph. The intuition behind solving this problem is to use Kosaraju's algorithm, which involves performing two depth-first search (DFS) traversals on the graph. The first DFS helps in finding the order of vertices based on their completion times, and the second DFS on the transposed graph helps in identifying the SCCs.

Note to remember: Kosaraju's algorithm is based on the idea that the SCCs in a graph correspond to the SCCs in its transposed graph, and the order of vertices obtained from the first DFS can be used to efficiently find the SCCs in the second DFS.

# Approach
1. Perform the first DFS traversal on the original graph:
   - Initialize a stack to store the vertices in the order of their completion times.
   - Start the DFS traversal from each unvisited vertex.
   - During the DFS, after exploring all the neighbors of a vertex, push the vertex onto the stack.

2. Transpose the graph:
   - Create a new adjacency list to represent the transposed graph.
   - Iterate over each edge `(u, v)` in the original graph and add the reverse edge `(v, u)` to the transposed graph.

3. Perform the second DFS traversal on the transposed graph:
   - Initialize a variable `count` to keep track of the number of SCCs.
   - Pop vertices from the stack obtained in step 1.
   - For each unvisited vertex, start a new DFS traversal.
   - During each DFS traversal, all the vertices visited belong to the same SCC.
   - Increment the `count` for each SCC found.

4. Return the `count` of strongly connected components.

# Complexity
- Time complexity: $O(V + E)$
  - The algorithm performs two DFS traversals and transposes the graph, each taking $O(V + E)$ time, where $V$ is the number of vertices and $E$ is the number of edges.
* Space complexity: $O(V)$
  - The space required for the stack, visited array, and transposed adjacency list is proportional to the number of vertices $V$.

# Code
```java
class Solution
{
    // Function to perform DFS traversal
    private void dfs(ArrayList<ArrayList<Integer>> adj, int v, boolean[] visited, Stack<Integer> stack) {
        visited[v] = true;
        
        for (int neighbor : adj.get(v)) {
            if (!visited[neighbor]) {
                dfs(adj, neighbor, visited, stack);
            }
        }
        
        stack.push(v);
    }
    
    // Function to obtain transpose of the graph
    private ArrayList<ArrayList<Integer>> transpose(ArrayList<ArrayList<Integer>> adj, int V) {
        ArrayList<ArrayList<Integer>> transposeAdj = new ArrayList<>();
        
        for (int i = 0; i < V; i++) {
            transposeAdj.add(new ArrayList<>());
        }
        
        for (int i = 0; i < V; i++) {
            for (int neighbor : adj.get(i)) {
                transposeAdj.get(neighbor).add(i);
            }
        }
        
        return transposeAdj;
    }
    
    //Function to find number of strongly connected components in the graph.
    public int kosaraju(int V, ArrayList<ArrayList<Integer>> adj)
    {
        // Step 1: Perform first DFS and push vertices onto stack
        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[V];
        Arrays.fill(visited, false);
        
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(adj, i, visited, stack);
            }
        }
        
        // Step 2: Transpose the graph
        ArrayList<ArrayList<Integer>> transposeAdj = transpose(adj, V);
        
        // Step 3: Perform second DFS on transposed graph
        Arrays.fill(visited, false);
        int count = 0; // Count of strongly connected components
        
        while (!stack.isEmpty()) {
            int v = stack.pop();
            if (!visited[v]) {
                dfs(transposeAdj, v, visited, new Stack<>());
                count++;
            }
        }
        
        return count;
    }
}
```