[Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem and a note to remember the solution -->
To serialize and deserialize a binary tree, we need to convert the tree into a string representation that can be easily stored or transmitted and then reconstruct the tree from that string representation. One approach is to use a preorder traversal to serialize the tree, where we visit each node and append its value to a string builder. For null nodes, we can use a special character (e.g., '#') to represent them. To deserialize the tree, we can split the string into an array of values and reconstruct the tree using a queue to simulate the preorder traversal.

# Approach
<!-- Describe your approach to solving the problem. -->
Serialization:
1. Define a helper function `serializeHelper(TreeNode node, StringBuilder sb)` that performs a preorder traversal of the binary tree.
2. In the `serializeHelper` function:
   - If the current node is null, append the special character '#' followed by a space to the string builder and return.
   - Append the value of the current node followed by a space to the string builder.
   - Recursively call `serializeHelper` on the left child of the current node.
   - Recursively call `serializeHelper` on the right child of the current node.
3. In the main function `serialize(TreeNode root)`, create an empty string builder, call the `serializeHelper` function with the root node and the string builder, and return the resulting string.

Deserialization:
1. In the `deserialize(String data)` function:
   - If the input string is empty, return null as there is no tree to deserialize.
   - Split the input string into an array of strings using the space delimiter.
   - Create a queue and initialize it with the array of strings.
   - Call the `deserializeHelper` function with the queue and return the reconstructed tree.
2. Define a helper function `deserializeHelper(Queue<String> queue)` that reconstructs the tree from the queue of values.
3. In the `deserializeHelper` function:
   - Poll the next value from the queue and store it in the variable `val`.
   - If `val` is equal to the special character '#', return null as it represents a null node.
   - Create a new `TreeNode` with the value of `val` parsed as an integer.
   - Recursively call `deserializeHelper` on the queue and assign the result to the left child of the current node.
   - Recursively call `deserializeHelper` on the queue and assign the result to the right child of the current node.
   - Return the reconstructed node.

# Complexity
- Time complexity: $O(n)$
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
Both the serialization and deserialization processes visit each node in the binary tree exactly once. Therefore, the time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(n)$
For serialization, the space complexity is determined by the size of the string builder used to store the serialized representation of the tree. In the worst case, the string builder will contain all the node values and the special characters, resulting in a space complexity of $O(n)$.
For deserialization, the space complexity is determined by the size of the queue used to store the node values. In the worst case, the queue will contain all the node values, resulting in a space complexity of $O(n)$.

# Code
### Preorder Traversal
```java
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serializeHelper(root, sb);
        return sb.toString();
    }

    private void serializeHelper(TreeNode node, StringBuilder sb) {
        if (node == null) {
            sb.append("# ");
            return;
        }

        sb.append(node.val).append(" ");
        serializeHelper(node.left, sb);
        serializeHelper(node.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.isEmpty()) {
            return null;
        }

        String[] nodes = data.split(" ");
        Queue<String> queue = new LinkedList<>(Arrays.asList(nodes));
        return deserializeHelper(queue);
    }

    private TreeNode deserializeHelper(Queue<String> queue) {
        String val = queue.poll();

        if (val.equals("#")) {
            return null;
        }

        TreeNode node = new TreeNode(Integer.parseInt(val));
        node.left = deserializeHelper(queue);
        node.right = deserializeHelper(queue);

        return node;
    }
}
```

### level Order Traversal
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) {
            return "";
        }

        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();

            if (node == null) {
                sb.append("# ");
                continue;
            }

            sb.append(node.val).append(" ");
            queue.offer(node.left);
            queue.offer(node.right);
        }

        return sb.toString().trim();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || data.isEmpty()) {
            return null;
        }

        String[] nodes = data.split(" ");
        TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        for (int i = 1; i < nodes.length; i++) {
            TreeNode parent = queue.poll();

            if (!nodes[i].equals("#")) {
                TreeNode left = new TreeNode(Integer.parseInt(nodes[i]));
                parent.left = left;
                queue.offer(left);
            }

            if (++i < nodes.length && !nodes[i].equals("#")) {
                TreeNode right = new TreeNode(Integer.parseInt(nodes[i]));
                parent.right = right;
                queue.offer(right);
            }
        }

        return root;
    }
}
```