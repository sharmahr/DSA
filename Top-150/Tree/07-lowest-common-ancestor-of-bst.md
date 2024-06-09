[Lowest Common Ancestor of BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)

# Intuition
The problem is to find the lowest common ancestor (LCA) of two nodes in a binary search tree (BST). In a BST, for any node, all the nodes in its left subtree have values smaller than the node's value, and all the nodes in its right subtree have values greater than the node's value. This property helps us efficiently search for the LCA. The LCA is the node where the two nodes p and q diverge in the tree.

# Approach
1. Start with the root node of the BST.
2. Compare the values of nodes p and q with the current node's value.
   - If both p and q have values smaller than the current node's value, the LCA lies in the left subtree of the current node. Recursively search in the left subtree.
   - If both p and q have values greater than the current node's value, the LCA lies in the right subtree of the current node. Recursively search in the right subtree.
   - If one node has a value smaller than the current node's value and the other node has a value greater than the current node's value, or if one of the nodes matches the current node, then the current node is the LCA. Return the current node.
3. Repeat step 2 until the LCA is found.

# Complexity
- Time complexity: $O(h)$
In the worst case, the time complexity is proportional to the height of the BST. In a balanced BST, the height is logarithmic, so the time complexity is $O(\log n)$, where $n$ is the number of nodes in the BST. However, in an unbalanced BST, the height can be linear, resulting in a time complexity of $O(n)$.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the BST is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the BST, which is $O(h)$, where $h$ is the height of the BST.

# Code
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // Given the tree is a BST

        // If both p and q are smaller than the current node, search in the left subtree
        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        } else if (p.val > root.val && q.val > root.val) {
            // If both p and q are greater than the current node, search in the right subtree
            return lowestCommonAncestor(root.right, p, q);
        } else {
            // If one node is smaller and the other node is larger, or if one node matches
            // the current node, then the current node is the lowest common ancestor
            return root;
        }
    }
}
```