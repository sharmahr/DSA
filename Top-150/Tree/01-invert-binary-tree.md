[Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)

# Intuition
The problem of inverting a binary tree can be solved by swapping the left and right child of each node. The intuition is to perform a level-order traversal of the tree using a queue and swap the left and right child of each node as we visit it. This approach ensures that all nodes in the tree are processed and their left and right children are swapped.

# Approach
1. Check if the root is null. If so, return null as there is no tree to invert.
2. Create a queue to perform a level-order traversal of the tree.
3. Enqueue the root node into the queue.
4. While the queue is not empty, do the following:
   - Dequeue a node from the queue.
   - If the node has a left child, enqueue the left child into the queue.
   - If the node has a right child, enqueue the right child into the queue.
   - Swap the left and right child of the current node.
5. After the while loop ends, the tree will be inverted.
6. Return the root of the inverted tree.

# Complexity
- Time complexity: $O(n)$
The level-order traversal visits each node in the tree exactly once. Therefore, the time complexity is linear in the number of nodes in the tree, which is $O(n)$, where $n$ is the number of nodes.

- Space complexity: $O(n)$
In the worst case, when the tree is a complete binary tree, the maximum number of nodes in the queue at any given time will be the nodes at the deepest level, which is approximately $n/2$. Therefore, the space complexity is $O(n)$ to store the queue.

# Code
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            
            if (node.left != null) {
                queue.offer(node.left);
            }
            if (node.right != null) {
                queue.offer(node.right);
            }
            
            // Swap the left and right child
            TreeNode temp = node.right;
            node.right = node.left;
            node.left = temp;
        }
        
        return root;
    }
}
```