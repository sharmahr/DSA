[Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/description/)

# Intuition
To find the right side view of a binary tree, we can perform a level order traversal (breadth-first search) and keep track of the rightmost node at each level. The rightmost node at each level will be the one visible from the right side. We can use a queue to perform the level order traversal and add the last node at each level to the result list.

# Approach
1. Create an empty list `result` to store the right side view of the binary tree.
2. If the root is null, return the empty list.
3. Create a queue `queue` and enqueue the root node.
4. While the queue is not empty, do the following:
   - Get the size of the queue, which represents the number of nodes at the current level.
   - Iterate `size` times:
     - Dequeue a node from the queue and assign it to the variable `head`.
     - If the current index `i` is equal to `size - 1` (i.e., it is the last node at the current level), add the value of `head` to `result`.
     - If `head` has a left child, enqueue the left child.
     - If `head` has a right child, enqueue the right child.
5. Return `result`, which contains the right side view of the binary tree.

# Complexity
- Time complexity: $O(n)$
We visit each node in the binary tree exactly once. The time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(m)$
The space complexity is determined by the maximum number of nodes at any level. In the worst case, when the binary tree is a complete binary tree, the maximum number of nodes at the deepest level is approximately $n/2$, where $n$ is the total number of nodes. Therefore, the space complexity is $O(m)$, where $m$ is the maximum number of nodes at any level.

# Code
```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size(); // this will process all the elements at the current level
            
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                if (i == size - 1) {
                    // process the last element of the queue
                    result.add(head.val);
                }
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
        }
        
        return result;
    }
}
```