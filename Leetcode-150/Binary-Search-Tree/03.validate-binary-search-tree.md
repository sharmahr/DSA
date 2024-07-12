[Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

# Intuition
To determine if a binary tree is a valid binary search tree (BST), we need to ensure that for each node, its value is greater than all the values in its left subtree and less than all the values in its right subtree. We can solve this problem using a recursive approach, where we keep track of the valid range for each node based on its ancestors. The valid range for a node is determined by the minimum and maximum values allowed for it to satisfy the BST property.

# Approach
1. Define a helper function `isValidBST(TreeNode node, long min, long max)` that takes the current node, the minimum value allowed, and the maximum value allowed as parameters.
2. If the current node is null, return true since an empty tree is considered a valid BST.
3. If the current node's value is less than or equal to the minimum value or greater than or equal to the maximum value, return false as it violates the BST property.
4. Recursively call `isValidBST` on the left subtree of the current node, passing the minimum value as `min` and the current node's value as `max`. This ensures that all values in the left subtree are less than the current node's value.
5. Recursively call `isValidBST` on the right subtree of the current node, passing the current node's value as `min` and the maximum value as `max`. This ensures that all values in the right subtree are greater than the current node's value.
6. Return the logical AND of the results from the recursive calls to the left and right subtrees. If both the left and right subtrees are valid BSTs, then the current tree is also a valid BST.
7. In the main function `isValidBST(TreeNode root)`, call the helper function with the root node, `Long.MIN_VALUE` as the minimum value, and `Long.MAX_VALUE` as the maximum value to cover the entire valid range.

# Complexity
- Time complexity: $O(n)$
We visit each node in the binary tree exactly once. The time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the binary tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the binary tree. In the best case, when the binary tree is balanced, the space complexity will be $O(\log n)$.

# Code
```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValidBST(TreeNode node, long min, long max) {
        if (node == null) {
            return true;
        }

        if (node.val <= min || node.val >= max) {
            return false;
        }

        return isValidBST(node.left, min, node.val) && isValidBST(node.right, node.val, max);
    }
}
```