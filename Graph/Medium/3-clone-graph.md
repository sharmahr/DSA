[Clone Graph](https://leetcode.com/problems/clone-graph/description/)

# Intuition
The problem asks to create a deep copy of a given graph. The intuition is to perform a depth-first search (DFS) traversal of the graph and create a cloned node for each visited node. We can use a hash map to keep track of the mapping between the original nodes and their cloned counterparts to avoid creating duplicate clones.

# Approach
1. If the given node is null, return null as there is no graph to clone.
2. Create a hash map `visited` to store the mapping between the original nodes and their cloned counterparts.
3. Implement a helper function `cloneGraph(Node node, Map<Integer, Node> visited)` that takes the current node and the `visited` map as parameters.
4. Inside the helper function:
   - Create a new cloned node with the same value as the current node.
   - Add the mapping between the current node's value and its cloned counterpart to the `visited` map.
   - Iterate through each neighbor of the current node:
     - If the neighbor has not been visited (not in the `visited` map), recursively call the helper function on the neighbor and add the returned cloned neighbor to the list of neighbors of the cloned node.
     - If the neighbor has already been visited (in the `visited` map), retrieve the cloned neighbor from the map and add it to the list of neighbors of the cloned node.
   - Set the `neighbors` of the cloned node to the list of cloned neighbors.
   - Return the cloned node.
5. Call the helper function with the given node and an empty `visited` map.
6. Return the cloned graph.

# Complexity
- Time complexity:
$$O(N + M)$$, where N is the number of nodes and M is the number of edges in the graph. We visit each node once and process each edge once.

- Space complexity:
$$O(N)$$ to store the `visited` map and the recursion stack. In the worst case, the recursion stack can go up to the depth of the graph.

# Code
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

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
        
        for (Node neighbor : node.neighbors) {
            if (!visited.containsKey(neighbor.val)) {
                clonedNode.neighbors.add(cloneGraph(neighbor, visited));
            } else {
                clonedNode.neighbors.add(visited.get(neighbor.val));
            }
        }
        
        return clonedNode;
    }
}
```

The code follows the approach described above. It first checks if the given node is null and returns null if so. It creates a `visited` map to store the mapping between the original nodes and their cloned counterparts. It then calls the helper function `cloneGraph(Node node, Map<Integer, Node> visited)` with the given node and the `visited` map. The helper function creates a new cloned node, adds it to the `visited` map, and recursively clones the neighbors of the current node. Finally, it returns the cloned node, which represents the cloned graph.