[Problem Statement](https://leetcode.com/problems/construct-string-from-binary-tree/description/)

# Intuition
The problem asks to construct a string representation of a binary tree. The intuition is to perform a preorder traversal of the tree and append the node values to the string. We need to include parentheses to represent the structure of the tree and handle the cases where a node has only a right child or no children.

# Approach
1. If the current node is null, return an empty string.
2. Convert the value of the current node to a string and append it to the result string.
3. If the current node has a left child:
   - Recursively convert the left subtree to a string and append it to the result string surrounded by parentheses.
4. If the current node has a right child:
   - Recursively convert the right subtree to a string and append it to the result string surrounded by parentheses.
5. If the current node has a right child but no left child:
   - Append an empty pair of parentheses "()" to represent the missing left child.
6. Return the result string.

# Complexity
- Time complexity:
$$O(n)$$, where n is the number of nodes in the binary tree. We visit each node once during the preorder traversal.

- Space complexity:
$$O(n)$$ in the worst case, where the tree is skewed and the recursion stack reaches the maximum depth of the tree.

# Code
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public String tree2str(TreeNode root) {
        if (root == null) {
            return "";
        }
        
        String result = Integer.toString(root.val);
        
        if (root.left != null) {
            result += "(" + tree2str(root.left) + ")";
        }
        
        if (root.right != null) {
            if (root.left == null) {
                result += "()";
            }
            result += "(" + tree2str(root.right) + ")";
        }
        
        return result;
    }
}
```