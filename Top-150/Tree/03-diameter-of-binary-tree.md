[Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)

# Intuition
To find the diameter of a binary tree, we need to consider three possibilities:
1. The diameter passes through the root node, in which case it is the sum of the heights of the left and right subtrees.
2. The diameter is entirely within the left subtree.
3. The diameter is entirely within the right subtree.

We can solve this problem using a recursive approach, where we calculate the heights of the left and right subtrees at each node and return the maximum diameter among the three possibilities.

# Approach
1. If the root is null, return 0 as the diameter of an empty tree is 0.
2. Calculate the height of the left subtree by calling the `heightOfTree` function on the left child of the root.
3. Calculate the height of the right subtree by calling the `heightOfTree` function on the right child of the root.
4. Recursively calculate the diameter of the left subtree by calling the `diameterOfBinaryTree` function on the left child of the root.
5. Recursively calculate the diameter of the right subtree by calling the `diameterOfBinaryTree` function on the right child of the root.
6. Return the maximum of the following three values:
   - The sum of the heights of the left and right subtrees (diameter passing through the root).
   - The diameter of the left subtree.
   - The diameter of the right subtree.

The `heightOfTree` function calculates the height of a subtree recursively:
1. If the root is null, return 0 as the height of an empty tree is 0.
2. Recursively calculate the height of the left subtree by calling the `heightOfTree` function on the left child of the root.
3. Recursively calculate the height of the right subtree by calling the `heightOfTree` function on the right child of the root.
4. Return 1 (to account for the current node) plus the maximum of the heights of the left and right subtrees.

# Complexity
- Time complexity: $O(n)$
The recursive approach visits each node in the tree exactly once. Therefore, the time complexity is linear in the number of nodes in the tree, which is $O(n)$, where $n$ is the number of nodes.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the tree. In the best case, when the tree is balanced, the maximum depth of the recursive calls will be $O(\log n)$.

# Code
```java
class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        if (root == null) return 0;

        int leftHeight = heightOfTree(root.left);
        int rightHeight = heightOfTree(root.right);

        int leftDiameter = diameterOfBinaryTree(root.left);
        int rightDiameter = diameterOfBinaryTree(root.right);

        // Return the maximum of (diameter of left subtree, diameter of right subtree, longest path through root)
        return Math.max(leftHeight + rightHeight, Math.max(leftDiameter, rightDiameter));
    }

    public int heightOfTree(TreeNode root) {
        if (root == null) return 0;

        int leftHeight = heightOfTree(root.left);
        int rightHeight = heightOfTree(root.right);

        // Height of the tree is 1 + maximum of heights of left and right subtrees
        return 1 + Math.max(leftHeight, rightHeight);
    }
}
```