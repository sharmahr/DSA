[Subtree of another Tree](https://leetcode.com/problems/subtree-of-another-tree/description/)

# Intuition
To determine if a tree is a subtree of another tree, we can recursively compare each node of the main tree with the root of the subtree. If we find a node in the main tree that is the same as the root of the subtree, we can then compare the entire subtree starting from that node. If any such comparison returns true, then the subtree exists within the main tree.

# Approach
1. Define a helper function `isSameTree` that takes two tree nodes `p` and `q` as input and returns true if the trees rooted at `p` and `q` are the same.
2. In the `isSubtree` function:
   - If the `root` is null, return false as an empty tree cannot contain any subtree.
   - Call the `isSameTree` function with `root` and `subRoot`. If it returns true, then the subtree rooted at `subRoot` exists within the main tree, so return true.
   - Recursively call `isSubtree` on the left child of `root` and `subRoot`. If it returns true, then the subtree exists in the left subtree of the main tree, so return true.
   - Recursively call `isSubtree` on the right child of `root` and `subRoot`. If it returns true, then the subtree exists in the right subtree of the main tree, so return true.
   - If none of the above conditions are met, return false.
3. In the `isSameTree` function:
   - If both `p` and `q` are null, return true as empty trees are considered the same.
   - If either `p` or `q` is null (but not both), return false as the trees are different.
   - If the values of `p` and `q` are not equal, return false as the trees are different.
   - Recursively call `isSameTree` on the left children of `p` and `q`, and on the right children of `p` and `q`. Return the logical AND of these recursive calls.

# Complexity
- Time complexity: $O(m * n)$
In the worst case, we need to compare each node of the main tree with the root of the subtree. For each comparison, we may need to compare the entire subtree. If the main tree has $m$ nodes and the subtree has $n$ nodes, the time complexity is $O(m * n)$.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the main tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the main tree, which is $O(h)$, where $h$ is the height of the main tree.

# Code
```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (root == null) {
            return false;
        }
        if (isSameTree(root, subRoot)) {
            return true;
        }
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }

    private boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        if (p.val != q.val) {
            return false;
        }
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```