[Remove Nth Node from the End](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

# Intuition
The problem is to remove the nth node from the end of a linked list. The intuition is to use two pointers, `first` and `second`, where `second` is initially ahead of `first` by `n` nodes. Then, move both pointers at the same pace until `second` reaches the end of the list. At this point, `first` will be pointing to the (n+1)th node from the end, and we can remove the next node (the nth node from the end).

# Approach
1. Create a dummy node and initialize `first` and `second` pointers to the dummy node.
2. Move the `second` pointer `n` steps ahead of the `first` pointer.
3. Move both `first` and `second` pointers until `second` reaches the end of the list.
4. Remove the next node after `first`, which is the nth node from the end.
5. Return the `next` node of the dummy node, which is the new head of the modified list.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
The time complexity is O(n), where n is the number of nodes in the linked list, as we need to traverse the list once. The space complexity is O(1) since we are using a constant amount of extra space (a few pointers).

# Code
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null) return null;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode first = dummy;
        ListNode second = dummy;

        // Move second ahead by n+1 steps to maintain the gap
        for (int i = 0; i <= n; i++) {
            second = second.next;
        }

        // Move both pointers until second reaches the end
        while (second != null) {
            first = first.next;
            second = second.next;
        }

        // Remove the nth node from the end
        first.next = first.next.next;
        return dummy.next;
    }
}
```