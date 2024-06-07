[Kahns Algorithm (Topological Sort using BFS)](https://www.geeksforgeeks.org/problems/topological-sort/1)

# Intuition
Topological sorting is an ordering of vertices in a directed acyclic graph (DAG) such that for every directed edge from vertex `u` to vertex `v`, vertex `u` comes before vertex `v` in the ordering. Another way to find the topological ordering is by using Kahn's algorithm, which involves calculating the in-degree of each vertex and iteratively removing vertices with in-degree 0 and their outgoing edges.

# Approach
1. Create a queue `queue` to store the vertices with in-degree 0.
2. Create an integer array `indegree` of size `V` to store the in-degree of each vertex.
3. Iterate through all the vertices from 0 to `V-1` and their adjacent vertices.
   - For each adjacent vertex `j` of vertex `i`, increment `indegree[j]` by 1.
4. Iterate through all the vertices from 0 to `V-1`.
   - If the in-degree of vertex `i` is 0, add it to the `queue`.
5. Create an integer array `result` of size `V` to store the final topological ordering.
6. Initialize an index variable `index` to 0.
7. While the `queue` is not empty, repeat the following steps:
   - Remove a vertex `front` from the front of the `queue`.
   - Store `front` in `result[index]` and increment `index` by 1.
   - Iterate through all the adjacent vertices of `front` using the adjacency list `adj.get(front)`.
     - For each adjacent vertex `i`, decrement `indegree[i]` by 1.
     - If `indegree[i]` becomes 0, add vertex `i` to the `queue`.
8. Return the `result` array containing the vertices in topological order.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - We iterate through all the vertices and edges once to calculate the in-degrees and perform the topological sorting.
* Space complexity: $O(V)$
  - The space required by the `queue`, `indegree` array, and `result` array is proportional to the number of vertices.

# Code
```java
class Solution{
    //Function to return list containing vertices in Topological order. 
    static int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) {
        // topological sorting is only valid for directed graph
        // if there is an arrow from u --> v then u will come first
        // the graph should be acyclic graph
        
        Queue<Integer> queue = new LinkedList<>();
        int[] indegree = new int[V];
        
        // fill the indegree array
        for(int i=0;i<V;i++){
            for(int j:adj.get(i)){
                indegree[j] += 1;
            }
        }
        
        // find the elements with indegree as 0
        for(int i=0;i<V;i++){
            if(indegree[i] == 0){
                queue.offer(i);
            }
        }
        int[] result = new int[V];
        
        //make the traversals
        int index = 0;
        while(!queue.isEmpty()){
            int front = queue.poll();
            result[index] = front;
            index += 1;
            for(int i:adj.get(front)){
                indegree[i] -= 1;
                if(indegree[i] == 0){
                    queue.offer(i);
                }
            }
        }
        
        return result;
    }
}
```