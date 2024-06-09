[Maximum Path Sum in a Binary Tree](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

# Intuition
To find the maximum path sum in a binary tree, we need to consider all possible paths and keep track of the maximum sum encountered. A path can start and end at any node, and it can either pass through the root or not. We can solve this problem using a recursive approach, where we calculate the maximum path sum for each node and update the overall maximum sum accordingly.

# Approach
1. Initialize an integer array `result` with a single element set to `Integer.MIN_VALUE`. This array will store the overall maximum path sum.
2. Define a recursive function `solve(TreeNode root, int[] result)` that returns the maximum path sum starting from the current node and updates the `result` array if necessary.
3. In the `solve` function:
   - If the current node is null, return 0 since an empty path has a sum of 0.
   - Recursively calculate the maximum path sum for the left subtree by calling `solve(root.left, result)`. If the result is negative, set it to 0 to ignore negative sums.
   - Recursively calculate the maximum path sum for the right subtree by calling `solve(root.right, result)`. If the result is negative, set it to 0 to ignore negative sums.
   - Calculate `temp` as the maximum of the left and right path sums plus the value of the current node. This represents the maximum path sum starting from the current node and continuing in one direction (either left or right).
   - Calculate `ans` as the maximum of `temp` and the sum of the left path sum, right path sum, and the value of the current node. This represents the maximum path sum that includes the current node and both its left and right subtrees.
   - Update `result[0]` with the maximum of its current value and `ans`. This keeps track of the overall maximum path sum.
   - Return `temp` as the maximum path sum starting from the current node.
4. In the main function `maxPathSum(TreeNode root)`, call the `solve` function with the root node and the `result` array, and return `result[0]`, which contains the maximum path sum.

# Complexity
- Time complexity: $O(n)$
The recursive function `solve` is called once for each node in the binary tree. Therefore, the time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(h)$
The space complexity is determined by the maximum depth of the recursive calls on the call stack. In the worst case, when the binary tree is skewed (i.e., each node has only one child), the maximum depth of the recursive calls will be equal to the height of the tree, which is $O(h)$, where $h$ is the height of the binary tree. In the best case, when the binary tree is balanced, the space complexity will be $O(\log n)$.

# Code
```java
class Solution {
    public int maxPathSum(TreeNode root) {
        int[] result = {Integer.MIN_VALUE};
        solve(root, result);
        return result[0];
    }

    int solve(TreeNode root, int[] result) {
        if (root == null) return 0;

        int left = Math.max(solve(root.left, result), 0); // Ignore negative sums
        int right = Math.max(solve(root.right, result), 0); // Ignore negative sums

        int temp = Math.max(left, right) + root.val;
        int ans = Math.max(temp, left + right + root.val);
        result[0] = Math.max(result[0], ans);

        return temp;
    }
}
```