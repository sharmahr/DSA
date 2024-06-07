[Problem Statement](https://leetcode.com/problems/remove-nodes-from-linked-list/description/)

# Intuition
The problem requires removing nodes from a linked list based on a specific condition: if a node has a value greater than or equal to any node to its right, it should be kept; otherwise, it should be removed. The intuition is to traverse the linked list from right to left and keep track of the maximum value encountered so far. If a node's value is less than the maximum value, it should be removed.

# Approach
1. First, check if the linked list is empty or contains only one node. In such cases, return the head as is.

2. Initialize an empty stack to store the nodes of the linked list.

3. Traverse the linked list from left to right and push each node onto the stack. This will reverse the order of the nodes, allowing us to process them from right to left.

4. Pop the top node from the stack and assign it as the initial `result` node. This will be the rightmost node that satisfies the condition.

5. Iterate through the remaining nodes in the stack:
   - Pop the top node from the stack and assign it to a temporary variable `temp`.
   - If `temp`'s value is greater than or equal to the `result`'s value, it means `temp` should be kept in the modified linked list.
     - Update `temp.next` to point to the current `result` node.
     - Update `result` to point to `temp`, effectively adding `temp` to the beginning of the modified linked list.

6. Return the `result` node, which represents the head of the modified linked list.

# Complexity
- Time complexity: O(n), where n is the number of nodes in the linked list. We traverse the linked list once to push all nodes onto the stack and then process each node once while popping from the stack.

- Space complexity: O(n) as we use a stack to store all the nodes of the linked list. In the worst case, when no nodes are removed, the stack will contain all n nodes.

# Code
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNodes(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        Stack<ListNode> stack = new Stack<>();
        ListNode current = head;

        // Push all nodes onto the stack
        while (current != null) {
            stack.push(current);
            current = current.next;
        }

        ListNode result = stack.pop();

        // Process nodes from right to left
        while (!stack.isEmpty()) {
            ListNode temp = stack.pop();
            if (temp.val >= result.val) {
                temp.next = result;
                result = temp;
            }
        }

        return result;
    }
}
```

This solution efficiently removes nodes from the linked list based on the given condition. By using a stack, we can process the nodes from right to left and keep track of the maximum value encountered. The time complexity is linear, and the space complexity is also linear in the worst case.