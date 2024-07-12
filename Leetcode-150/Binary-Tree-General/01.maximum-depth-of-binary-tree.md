[Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

# Intuition
To find the maximum depth of a binary tree, we can use a recursive approach. The intuition is that the maximum depth of a tree is the maximum depth of its left subtree or its right subtree, plus one (to account for the root node). We can recursively traverse the tree, calculate the maximum depth of the left and right subtrees, and return the maximum of the two depths plus one.

# Approach
1. Check if the root is null. If so, return 0 as the maximum depth of an empty tree is 0.
2. Initialize two variables, `left` and `right`, to store the maximum depths of the left and right subtrees, respectively.
3. If the root has a left child, recursively call the `maxDepth` function on the left child and assign the result to `left`.
4. If the root has a right child, recursively call the `maxDepth` function on the right child and assign the result to `right`.
5. Return 1 (to account for the root node) plus the maximum of `left` and `right`.

# Complexity
- Time complexity: $O(n)$
The recursive approach visits each node in the tree exactly once. Therefore, the time complexity is linear in the number of nodes in the tree, which is $O(n)$, where $n$ is the number of nodes.

- Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the tree. In the best case, when the tree is balanced, the maximum depth of the recursive calls will be $O(\log n)$.

# Code
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int left = 0;
        int right = 0;
        
        if (root.left != null) {
            left = maxDepth(root.left);
        }
        if (root.right != null) {
            right = maxDepth(root.right);
        }
        
        return 1 + Math.max(left, right);
    }
}
```