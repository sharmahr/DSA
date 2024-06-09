[Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)

# Intuition
To perform level order traversal of a binary tree, we can use a breadth-first search (BFS) approach using a queue. The idea is to process the nodes level by level, starting from the root. At each level, we enqueue the nodes from left to right and process them in the order they were enqueued. This ensures that we visit the nodes in level order.

# Approach
1. Create an empty list `list` to store the level order traversal result.
2. If the root is null, return the empty list.
3. Create a queue `queue` and enqueue the root node.
4. While the queue is not empty, do the following:
   - Create a temporary list `tempList` to store the nodes at the current level.
   - Get the size of the queue, which represents the number of nodes at the current level.
   - Iterate `size` times:
     - Dequeue a node from the queue and add its value to `tempList`.
     - If the dequeued node has a left child, enqueue the left child.
     - If the dequeued node has a right child, enqueue the right child.
   - Add `tempList` to `list`.
5. Return `list`, which contains the level order traversal of the binary tree.

# Complexity
- Time complexity: $O(n)$
We visit each node in the binary tree exactly once. The time complexity is linear in the number of nodes, which is $O(n)$, where $n$ is the number of nodes in the binary tree.

* Space complexity: $O(m)$
The space complexity is determined by the maximum number of nodes at any level. In the worst case, when the binary tree is a complete binary tree, the maximum number of nodes at the deepest level is approximately $n/2$, where $n$ is the total number of nodes. Therefore, the space complexity is $O(m)$, where $m$ is the maximum number of nodes at any level.

# Code
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();
        if (root == null) return list;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            List<Integer> tempList = new ArrayList<>();
            int size = queue.size();
            
            for (int i = 0; i < size; i++) {
                TreeNode temp = queue.poll();
                tempList.add(temp.val);
                
                if (temp.left != null) {
                    queue.offer(temp.left);
                }
                if (temp.right != null) {
                    queue.offer(temp.right);
                }
            }
            
            list.add(tempList);
        }
        
        return list;
    }
}
```