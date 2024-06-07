[Topological Sort using DFS](https://www.geeksforgeeks.org/problems/topological-sort/1)

# Intuition
Topological sorting is an ordering of vertices in a directed acyclic graph (DAG) such that for every directed edge from vertex `u` to vertex `v`, vertex `u` comes before vertex `v` in the ordering. One way to find the topological ordering is by using depth-first search (DFS) and storing the vertices in a stack in the order of their completion times.

# Approach
1. Create a stack `stack` to store the vertices in their completion order.
2. Create a boolean array `visited` of size `V` to keep track of visited vertices.
3. Create an integer array `result` of size `V` to store the final topological ordering.
4. Iterate through all the vertices from 0 to `V-1`.
   - If vertex `i` is not visited, call the `topologicalSortHelper` function to perform DFS starting from vertex `i`.
5. In the `topologicalSortHelper` function:
   - Mark the current vertex `u` as visited.
   - Iterate through all the adjacent vertices of `u` using the adjacency list `adj.get(u)`.
     - If an adjacent vertex `i` is not visited, recursively call `topologicalSortHelper` for vertex `i`.
   - After exploring all the adjacent vertices, push the current vertex `u` onto the `stack`.
6. After the DFS traversal is complete, pop the vertices from the `stack` and store them in the `result` array.
7. Return the `result` array containing the vertices in topological order.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The DFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `visited` array, `stack`, and `result` array is proportional to the number of vertices.
  - The recursion stack can go up to a depth of `V` in the worst case.

# Code
```java
class Solution{
    //Function to return list containing vertices in Topological order. 
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) {
        // topological sorting is only valid for directed graph
        // if there is an arrow from u --> v then u will come first
        // the graph should be acyclic graph
        
        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[V];
        int[] result = new int[V];
        
        for(int i=0;i<V;i++){
            if(!visited[i]){
                topologicalSortHelper(adj, i, stack, visited);
            }
        }
        
        for(int i=0;i<V;i++){
            result[i] = stack.pop();
        }
        return result;
    }
    
    static void topologicalSortHelper(ArrayList<ArrayList<Integer>> adj, int u, Stack<Integer> stack, boolean[] visited){
        visited[u] = true;
        for(int i:adj.get(u)){
            if(!visited[i]){
                topologicalSortHelper(adj, i, stack, visited);
            }
        }
        stack.push(u);
    }
    
}
```