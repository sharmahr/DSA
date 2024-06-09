[Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)

# Intuition
To find the kth smallest element in a binary search tree (BST), we can leverage the property of BSTs: in-order traversal of a BST yields the elements in ascending order. By performing an in-order traversal and storing the elements in a list, we can easily retrieve the kth smallest element by accessing the element at index k-1 in the list.

# Approach
1. Create an empty ArrayList called `list` to store the elements of the BST in ascending order.
2. Perform an in-order traversal of the BST using a helper function `inorderTraversal(TreeNode root, ArrayList<Integer> list)`.
3. In the `inorderTraversal` function:
   - If the current node is null, return as there are no elements to process.
   - Recursively traverse the left subtree by calling `inorderTraversal(root.left, list)`.
   - Add the value of the current node to the `list`.
   - Recursively traverse the right subtree by calling `inorderTraversal(root.right, list)`.
4. After the in-order traversal is complete, the `list` will contain the elements of the BST in ascending order.
5. Return the element at index k-1 in the `list`, which represents the kth smallest element in the BST.

# Complexity
- Time complexity: $O(n)$
The in-order traversal visits each node in the BST exactly once, so the time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the BST.

* Space complexity: $O(n)$
The space complexity is determined by the size of the `list` used to store the elements of the BST. In the worst case, when we need to store all the elements of the BST, the space complexity is $O(n)$, where $n$ is the number of nodes in the BST.

# Code
```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        ArrayList<Integer> list = new ArrayList<>();
        inorderTraversal(root, list);
        return list.get(k - 1);
    }

    public void inorderTraversal(TreeNode root, ArrayList<Integer> list) {
        if (root == null) return;
        inorderTraversal(root.left, list);
        list.add(root.val);
        inorderTraversal(root.right, list);
    }
}
```