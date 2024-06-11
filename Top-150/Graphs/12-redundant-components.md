[Redundant Components](https://leetcode.com/problems/redundant-connection/description/)

# Intuition
To find the redundant connection in the given graph, we can use a disjoint set data structure (also known as a union-find data structure). By iterating through the edges and performing union operations, we can detect the edge that forms a cycle in the graph. The last edge that causes a cycle is the redundant connection.

# Approach
1. Initialize a `parent` array to represent the disjoint set data structure. Each node is initially its own parent.
2. Iterate through each edge in the `edges` array:
   - Find the parent of both nodes of the current edge using the `find` function.
   - If the parent of both nodes is the same, it means adding this edge will form a cycle. Return the current edge as the redundant connection.
   - Otherwise, perform a union operation on the two nodes using the `union` function to merge their sets.
3. If no redundant connection is found after iterating through all edges, return an empty array.

The `find` function performs path compression to find the parent of a node. It recursively finds the parent of a node until it reaches the root node (i.e., a node whose parent is itself).

The `union` function merges the sets of two nodes by updating the parent of one node's root to be the other node's root.

# Complexity
- Time complexity: O(N * α(N))
  - N is the number of nodes in the graph.
  - α is the inverse Ackermann function, which grows very slowly and is nearly constant for all practical purposes.
  - The `find` function uses path compression, which makes the time complexity nearly linear.
  - The `union` function also takes almost constant time on average.
- Space complexity: O(N)
  - The `parent` array requires O(N) space to store the parent of each node.

# Code
```java
class Solution {
    int[] parent;

    public int[] findRedundantConnection(int[][] edges) {
        parent = new int[edges.length];
        for (int i = 0; i < edges.length; i++) {
            parent[i] = i + 1;
        }

        for (int[] edge : edges) {
            if (find(edge[0]) == find(edge[1])) {
                return edge;
            } else {
                union(edge[0], edge[1]);
            }
        }

        return new int[2];
    }

    public int find(int x) {
        if (x == parent[x - 1]) {
            return x;
        }
        return parent[x - 1] = find(parent[x - 1]);
    }

    public void union(int x, int y) {
        parent[find(y) - 1] = find(x);
    }
}
```