[Construct Binary Tree from Inorder and Preorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

# Intuition
To construct the binary tree from its preorder and inorder traversals, we can utilize the properties of these traversals. In the preorder traversal, the first element represents the root node, followed by the elements of the left subtree and then the elements of the right subtree. In the inorder traversal, the elements are in the order of left subtree, root, and right subtree. By combining the information from both traversals, we can uniquely determine the structure of the binary tree.

# Approach
1. Create a HashMap called `inorderMap` to store the mapping of values to their indices in the inorder traversal array. This will allow us to efficiently locate the root index in the inorder array.
2. Iterate through the inorder array and populate the `inorderMap` with the values as keys and their indices as values.
3. Initialize a variable `preorderIndex` to keep track of the current index in the preorder array.
4. Define a recursive function `buildTree(int[] preorder, int start, int end)` that takes the preorder array, the start index, and the end index of the current subtree in the inorder array.
5. In the `buildTree` function:
   - If the start index is greater than the end index, return null as there are no elements to construct the subtree.
   - Get the root value from the preorder array at the current `preorderIndex` and increment the `preorderIndex`.
   - Create a new TreeNode called `root` with the root value.
   - Retrieve the index of the root value in the inorder array using the `inorderMap`.
   - Recursively build the left subtree by calling `buildTree(preorder, start, rootIndex - 1)`.
   - Recursively build the right subtree by calling `buildTree(preorder, rootIndex + 1, end)`.
   - Return the constructed `root` node.
6. In the main function `buildTree(int[] preorder, int[] inorder)`, call the recursive `buildTree` function with the preorder array, start index as 0, and end index as `preorder.length - 1`.

# Complexity
- Time complexity: $O(n)$
The recursive `buildTree` function is called once for each node in the binary tree. The HashMap operations (put and get) have an average time complexity of $O(1)$. Therefore, the overall time complexity is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(n)$
The space complexity is determined by the space used by the `inorderMap` and the recursive call stack. The `inorderMap` stores all the elements of the inorder array, so its space complexity is $O(n)$. The recursive call stack can go up to a depth of $O(n)$ in the worst case (skewed tree). Therefore, the overall space complexity is $O(n)$.

# Code
```java
class Solution {
    int preorderIndex = 0;
    Map<Integer, Integer> inorderMap = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return buildTree(preorder, 0, preorder.length - 1);
    }

    private TreeNode buildTree(int[] preorder, int start, int end) {
        if (start > end) {
            return null;
        }
        int rootVal = preorder[preorderIndex];
        preorderIndex++;
        TreeNode root = new TreeNode(rootVal);

        int rootIndex = inorderMap.get(rootVal);
        root.left = buildTree(preorder, start, rootIndex - 1); // build the left subtree
        root.right = buildTree(preorder, rootIndex + 1, end); // build the right subtree
        return root;
    }
}
```