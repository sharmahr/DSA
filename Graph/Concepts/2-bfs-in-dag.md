[BFS Of Directed Acylic Graph](https://www.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)

# Intuition
The problem requires performing a Breadth-First Search (BFS) traversal on a given graph represented by an adjacency list. BFS explores the graph level by level, visiting all the vertices at the current level before moving on to the next level. It uses a queue to keep track of the vertices to be visited.

# Approach
1. Create an ArrayList `result` to store the BFS traversal order of the vertices.
2. Create a boolean array `visited` to keep track of visited vertices.
3. Create a queue `queue` to store the vertices to be visited.
4. Enqueue the starting vertex (0 in this case) into the `queue` and mark it as visited.
5. While the `queue` is not empty, repeat the following steps:
   - Dequeue a vertex `front` from the `queue`.
   - Add the vertex `front` to the `result` list.
   - Iterate through all the adjacent vertices of `front` using the adjacency list `adj.get(front)`.
   - For each unvisited adjacent vertex `i`:
     - Mark vertex `i` as visited.
     - Enqueue vertex `i` into the `queue`.
6. Return the `result` list containing the BFS traversal order.

# Complexity
- Time complexity: $O(V + E)$
  - Where V is the number of vertices and E is the number of edges in the graph.
  - The BFS traversal visits each vertex once and explores all the edges.
* Space complexity: $O(V)$
  - The space required by the `visited` array and the `queue` is proportional to the number of vertices.

# Code
```java
class Solution {
    // Function to return Breadth First Traversal of given graph.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        ArrayList<Integer> result = new ArrayList<>();
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(0);
        visited[0] = true;
        
        while(!queue.isEmpty()){
            int front = queue.poll();
            result.add(front);
            for(int i:adj.get(front)){
                if(!visited[i]){
                    visited[i] = true;
                    queue.offer(i);
                }
            }
        }
        return result;
    }
}
```