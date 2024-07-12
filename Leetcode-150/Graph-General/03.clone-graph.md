[Clone Graph](https://leetcode.com/problems/clone-graph/description/)

# Intuition
To clone a graph, we can use a depth-first search (DFS) approach along with a hash map to keep track of visited nodes. The hash map will store the mapping between the original node and its cloned counterpart. We can recursively clone each node and its neighbors while avoiding duplicate cloning by checking the hash map.

# Approach
1. Check if the input `node` is null. If so, return null as there is no graph to clone.
2. Create a hash map `visited` to store the mapping between the original nodes and their cloned counterparts.
3. Call the recursive helper function `cloneGraph(node, visited)` to clone the graph starting from the given node.
4. In the recursive helper function:
   - Create a new cloned node `clonedNode` with the same value as the original node.
   - Add the mapping between the original node's value and the cloned node to the `visited` hash map.
   - Create an empty list `clonedNeighbors` to store the cloned neighbors of the current node.
   - Iterate through each neighbor of the original node:
     - If the neighbor has not been visited (not present in the hash map), recursively clone the neighbor and add the cloned neighbor to `clonedNeighbors`.
     - If the neighbor has already been visited (present in the hash map), retrieve the cloned neighbor from the hash map and add it to `clonedNeighbors`.
   - Set the `neighbors` of the cloned node to `clonedNeighbors`.
   - Return the cloned node.
5. The recursive calls will ensure that all nodes and their neighbors are cloned properly.

# Complexity
- Time complexity: O(N + M)
  - N is the number of nodes in the graph.
  - M is the total number of edges (neighbors) in the graph.
  - Each node is visited once, and each neighbor is processed once.
- Space complexity: O(N)
  - The space complexity is determined by the recursion stack and the hash map.
  - In the worst case, the recursion stack can go up to the depth of the graph, which is at most N.
  - The hash map stores a mapping for each node, so it requires O(N) space.

# Code
```java
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) {
            return null;
        }
        Map<Integer, Node> visited = new HashMap<>();
        return cloneGraph(node, visited);
    }

    private Node cloneGraph(Node node, Map<Integer, Node> visited) {
        Node clonedNode = new Node(node.val);
        visited.put(node.val, clonedNode);

        List<Node> clonedNeighbors = new ArrayList<>();
        for (Node neighbor : node.neighbors) {
            if (!visited.containsKey(neighbor.val)) {
                clonedNeighbors.add(cloneGraph(neighbor, visited));
            } else {
                clonedNeighbors.add(visited.get(neighbor.val));
            }
        }
        clonedNode.neighbors = clonedNeighbors;

        return clonedNode;
    }
}
```