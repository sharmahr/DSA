[Number of Connected Components](https://neetcode.io/problems/count-connected-components)

# Intuition
To count the number of connected components in an undirected graph, we can perform depth-first search (DFS) on each unvisited node. Each DFS traversal will explore a single connected component, and the total number of DFS traversals will give us the count of connected components.

# Approach
1. Create an adjacency list representation of the graph using the given edges.
2. Create a boolean array `visited` to keep track of visited nodes.
3. Initialize a variable `count` to 0 to store the count of connected components.
4. Iterate through each node in the graph:
   - If the node is not visited, perform DFS starting from that node.
   - Increment `count` by 1 after each DFS traversal.
5. Return `count` as the total number of connected components.

In the DFS function:
1. Mark the current node as visited.
2. Iterate through the neighbors of the current node.
3. If a neighbor is not visited, recursively perform DFS on that neighbor.

# Complexity
- Time complexity: O(N + E)
  - N is the number of nodes in the graph.
  - E is the number of edges in the graph.
  - The DFS traversal visits each node and edge once.
- Space complexity: O(N)
  - The adjacency list representation of the graph requires O(N) space.
  - The recursion stack in DFS can go up to a depth of N in the worst case.

# Code
```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        // Create the adjacency list and the boolean array
        boolean[] visited = new boolean[n];
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            adjacencyList.get(u).add(v);
            adjacencyList.get(v).add(u);
        }

        // Perform DFS
        int count = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i, adjacencyList, visited);
                count++;
            }
        }

        return count;
    }

    private void dfs(int node, List<List<Integer>> adjacencyList, boolean[] visited) {
        visited[node] = true;
        for (int neighbor : adjacencyList.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adjacencyList, visited);
            }
        }
    }
}
```