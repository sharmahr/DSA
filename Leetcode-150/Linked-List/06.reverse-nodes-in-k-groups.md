[Reverse Nodes in K groups](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)

# Intuition
The problem is to reverse nodes in a linked list in groups of size `k`. The intuition is to use a recursive approach to reverse the first `k` nodes of the linked list, and then move to the next group of `k` nodes and repeat the process. We can keep track of the next group's starting node by maintaining a reference to the node right after the current group.

# Approach
1. Define a helper function `reverseKGroup` that takes the head of the linked list and the value of `k` as input.
2. In the `reverseKGroup` function:
   a. Check if the linked list is empty or has fewer than `k` nodes. If so, return the head as is.
   b. Initialize a pointer `prev` to keep track of the node before the current group of `k` nodes.
   c. Initialize a pointer `curr` to keep track of the current node in the current group.
   d. Reverse the first `k` nodes of the linked list using a standard reversal algorithm.
   e. Recursively call `reverseKGroup` with the node after the current group of `k` nodes as the new head, and the same value of `k`.
   f. Connect the reversed group of `k` nodes with the next group of `k` nodes returned from the recursive call.
   g. Return the new head of the modified linked list.
3. In the main function `reverseKGroup`, call the helper function `reverseKGroup` with the given head and the value of `k`.

# Complexity
- Time complexity: O(n)
* Space complexity: O(n/k)
The time complexity is O(n), where n is the number of nodes in the linked list, because we need to traverse the entire list once to reverse the nodes in groups of size `k`. The space complexity is O(n/k) because the maximum depth of the recursion stack is n/k, where each recursive call stores a constant amount of data.

# Code
```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k == 1) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;

        int count = 0;
        ListNode curr = head;

        // Count the number of nodes in the linked list
        while (curr != null) {
            curr = curr.next;
            count++;
        }

        curr = head;

        // Reverse the linked list in groups of size k
        while (count >= k) {
            ListNode prevGroupTail = prev;
            for (int i = 1; i < k; i++) {
                ListNode temp = curr.next;
                curr.next = temp.next;
                temp.next = prev.next;
                prev.next = temp;
            }
            prev = curr;
            count -= k;
            curr = curr.next;
        }

        return dummy.next;
    }
}
```