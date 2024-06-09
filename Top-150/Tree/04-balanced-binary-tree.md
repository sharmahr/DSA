[Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)

# Intuition
To determine if a binary tree is balanced, we need to check if the heights of the left and right subtrees of each node differ by at most 1. We can solve this problem using a recursive approach, where we calculate the heights of the left and right subtrees at each node and check if their difference is within the allowed range. If at any point the difference exceeds 1, the tree is not balanced.

# Approach
1. Define a helper function `checkHeight` that takes a node as input and returns the height of the subtree rooted at that node.
2. In the `isBalanced` function, call `checkHeight` on the root node and return true if the result is not -1, indicating that the tree is balanced.
3. In the `checkHeight` function:
   - If the node is null, return 0 as the height of an empty subtree is 0.
   - Recursively call `checkHeight` on the left child of the node and store the result in `leftHeight`.
   - If `leftHeight` is -1, return -1 as the tree is not balanced.
   - Recursively call `checkHeight` on the right child of the node and store the result in `rightHeight`.
   - If `rightHeight` is -1, return -1 as the tree is not balanced.
   - If the absolute difference between `leftHeight` and `rightHeight` is greater than 1, return -1 as the tree is not balanced.
   - Otherwise, return 1 (to account for the current node) plus the maximum of `leftHeight` and `rightHeight`.

# Complexity
- Time complexity: $O(n)$
The recursive approach visits each node in the tree exactly once. Therefore, the time complexity is linear in the number of nodes in the tree, which is $O(n)$, where $n$ is the number of nodes.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the tree. In the best case, when the tree is balanced, the maximum depth of the recursive calls will be $O(\log n)$.

# Code
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return checkHeight(root) != -1;
    }

    private int checkHeight(TreeNode node) {
        if (node == null) {
            return 0;
        }

        int leftHeight = checkHeight(node.left);
        if (leftHeight == -1) {
            return -1;
        }

        int rightHeight = checkHeight(node.right);
        if (rightHeight == -1) {
            return -1;
        }

        if (Math.abs(leftHeight - rightHeight) > 1) {
            return -1;
        }

        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```