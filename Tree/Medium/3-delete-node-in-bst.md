[Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/description/)

# Intuition
The problem asks to delete a node with a given key from a Binary Search Tree (BST). The intuition is to recursively traverse the BST to find the node to be deleted and handle different cases based on the number of children the node has.

# Approach
1. If the root is null, return null as the tree is empty.
2. If the key is less than the current node's value:
   - Recursively call the function on the left subtree to delete the node.
   - Update the left child of the current node with the result of the recursive call.
3. If the key is greater than the current node's value:
   - Recursively call the function on the right subtree to delete the node.
   - Update the right child of the current node with the result of the recursive call.
4. If the key is equal to the current node's value (node to be deleted):
   - Case 1: If the node is a leaf node (has no children), return null to delete the node.
   - Case 2: If the node has only one child, return the child to replace the node.
   - Case 3: If the node has two children:
     - Find the minimum node in the right subtree (inorder successor).
     - Replace the value of the current node with the value of the inorder successor.
     - Recursively delete the inorder successor from the right subtree.
5. Return the root of the modified BST.

# Complexity
- Time complexity:
$$O(h)$$, where h is the height of the BST. In the worst case, when the BST is skewed and resembles a linked list, the time complexity can be $$O(n)$$, where n is the number of nodes in the BST.

- Space complexity:
$$O(h)$$ in the worst case due to the recursion stack. The space complexity is proportional to the height of the BST.

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            // Case 1: If the node is a leaf node
            if (root.left == null && root.right == null) {
                return null;
            }
            
            // Case 2: If the node has only one child
            if (root.left == null) {
                return root.right;
            } else if (root.right == null) {
                return root.left;
            }
            
            // Case 3: If the node has two children
            TreeNode successor = findMinNode(root.right);
            root.val = successor.val;
            root.right = deleteNode(root.right, successor.val);
        }
        
        return root;
    }
    
    private TreeNode findMinNode(TreeNode node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }
}
```