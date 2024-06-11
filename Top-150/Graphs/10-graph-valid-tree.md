[Graph Valid Tree](https://neetcode.io/problems/valid-tree)

# Intuition
To determine if a given graph is a valid tree, we need to check two conditions:
1. The graph must contain exactly n - 1 edges, where n is the number of nodes.
2. The graph must be fully connected, meaning there is a path between any two nodes, and there are no cycles.

We can use depth-first search (DFS) to traverse the graph and check for connectivity and cycles.

# Approach
1. Check if the number of edges is equal to n - 1. If not, return false.
2. Create an adjacency list representation of the graph using the given edges.
3. Perform DFS starting from any node (e.g., node 0) to check for connectivity and cycles:
   - Mark the current node as visited.
   - Iterate through the neighbors of the current node.
   - If a neighbor is not visited, recursively perform DFS on that neighbor, passing the current node as the parent.
   - If a neighbor is already visited and it is not the parent of the current node, it means there is a cycle, so return false.
4. After the DFS traversal, ensure that all nodes are visited. If any node is not visited, it means the graph is not connected, so return false.
5. If all conditions are satisfied, return true.

# Complexity
- Time complexity: O(n)
  - The DFS traversal visits each node once.
  - Creating the adjacency list takes O(n) time.
- Space complexity: O(n)
  - The adjacency list representation of the graph requires O(n) space.
  - The recursion stack in DFS can go up to a depth of n in the worst case.

# Code
```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        // Condition 1: The graph must contain exactly n - 1 edges
        if (edges.length != n - 1) return false;

        // Condition 2: The graph must be fully connected
        // Create an adjacency list for the graph
        List<List<Integer>> adjacencyList = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            adjacencyList.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            adjacencyList.get(edge[0]).add(edge[1]);
            adjacencyList.get(edge[1]).add(edge[0]);
        }

        // Perform DFS to check for connectivity and detect cycles
        boolean[] visited = new boolean[n];
        if (!dfs(0, -1, visited, adjacencyList)) return false;

        // Ensure all nodes are visited (the graph is connected)
        for (boolean v : visited) {
            if (!v) return false;
        }

        return true;
    }

    private boolean dfs(int node, int parent, boolean[] visited, List<List<Integer>> adjacencyList) {
        visited[node] = true;
        for (int neighbor : adjacencyList.get(node)) {
            if (!visited[neighbor]) {
                if (!dfs(neighbor, node, visited, adjacencyList)) return false;
            } else if (neighbor != parent) {
                return false; // Cycle detected
            }
        }
        return true;
    }
}
```