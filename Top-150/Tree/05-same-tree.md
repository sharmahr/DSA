[Same Tree](https://leetcode.com/problems/same-tree/description/)

# Intuition
To determine if two binary trees are the same, we can compare their structure and node values. One approach is to perform an inorder traversal of both trees and store the node values in separate lists. If the resulting lists are equal, the trees are the same. However, this approach has some limitations, as it only compares the node values and not the actual structure of the trees.

# Approach
1. Define a helper function `inorder` that takes a tree node as input and returns an ArrayList containing the node values in inorder traversal order.
2. In the `isSameTree` function, call the `inorder` function on both trees `p` and `q` to obtain their inorder traversal lists `listp` and `listq`, respectively.
3. Compare `listp` and `listq` using the `equals` method of ArrayList. If the lists are equal, return true; otherwise, return false.
4. In the `inorder` function:
   - Create an empty ArrayList called `list` to store the node values.
   - If the current node is null, return the empty list.
   - Recursively call `inorder` on the left child of the current node and add the resulting list to `list` using `addAll`.
   - Add the value of the current node to `list`.
   - Recursively call `inorder` on the right child of the current node and add the resulting list to `list` using `addAll`.
   - Return the `list` containing the inorder traversal of the subtree rooted at the current node.

# Complexity
- Time complexity: $O(n)$
The inorder traversal visits each node in the tree exactly once. Therefore, the time complexity is linear in the number of nodes in the tree, which is $O(n)$, where $n$ is the number of nodes.

* Space complexity: $O(n)$
The space complexity is determined by the space required to store the inorder traversal lists. In the worst case, when the trees are skewed (i.e., each node has only one child), the size of the lists will be equal to the number of nodes in the tree, which is $O(n)$. In the best case, when the trees are balanced, the size of the lists will be $O(\log n)$.

# Code
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        ArrayList<Integer> listp = inorder(p);
        ArrayList<Integer> listq = inorder(q);
        return listq.equals(listp);
    }

    public ArrayList<Integer> inorder(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<>();
        if (root == null) return list;
        list.addAll(inorder(root.left));
        list.add(root.val);
        list.addAll(inorder(root.right));
        return list;
    }
}
```

However, it's important to note that this approach has limitations. It only compares the node values and not the actual structure of the trees. Two trees with the same inorder traversal may have different structures. A more accurate approach would be to recursively compare the nodes and their left and right subtrees.

Here's an alternative solution that compares the structure and values of the trees recursively:

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        if (p.val != q.val) return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

This recursive approach has a time complexity of $O(n)$ and a space complexity of $O(h)$, where $n$ is the number of nodes and $h$ is the height of the tree.