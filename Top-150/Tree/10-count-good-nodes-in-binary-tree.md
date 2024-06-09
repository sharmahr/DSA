[Count Of Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/description/)

# Intuition
To count the number of good nodes in a binary tree, we can perform a depth-first search (DFS) traversal and keep track of the maximum value encountered so far along each path. If the current node's value is greater than or equal to the maximum value seen so far, it is considered a good node. We can recursively traverse the tree and update the maximum value at each step.

# Approach
1. Define a helper function `goodNodes(TreeNode root, int max)` that takes the current node and the maximum value encountered so far as parameters.
2. If the current node is null, return 0 since an empty tree has no good nodes.
3. Update the `max` variable to be the maximum of the current node's value and the previous `max` value.
4. Recursively call `goodNodes` on the left and right subtrees, passing the updated `max` value.
5. Store the sum of the good nodes in the left and right subtrees in the `result` variable.
6. If the current node's value is greater than or equal to `max`, increment `result` by 1 to count the current node as a good node.
7. Return `result`, which represents the total count of good nodes in the current subtree.
8. In the main function `goodNodes(TreeNode root)`, call the helper function with the root node and the initial `max` value set to `Integer.MIN_VALUE` to ensure that the root node is always considered a good node.

# Complexity
- Time complexity: $O(n)$
We visit each node in the binary tree exactly once. The time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the binary tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the binary tree. In the best case, when the binary tree is balanced, the space complexity will be $O(\log n)$.

# Code
```java
class Solution {
    public int goodNodes(TreeNode root) {
        return goodNodes(root, Integer.MIN_VALUE);
    }

    private int goodNodes(TreeNode root, int max) {
        if (root == null) return 0;
        
        max = Math.max(root.val, max);
        int left = goodNodes(root.left, max);
        int right = goodNodes(root.right, max);
        int result = left + right;
        
        if (root.val >= max) {
            result++;
        }
        
        return result;
    }
}
```