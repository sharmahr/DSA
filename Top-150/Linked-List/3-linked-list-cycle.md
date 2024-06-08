[Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)


# Intuition
The problem is to determine if a given linked list contains a cycle. The intuition is to use the Floyd's cycle-finding algorithm, also known as the "tortoise and hare" algorithm. The idea is to use two pointers, one moving twice as fast as the other. If there is a cycle, the two pointers will eventually meet. If there is no cycle, the faster pointer will reach the end of the list first.

# Approach
1. Check if the head or the next node is null. If so, return false (no cycle).
2. Initialize two pointers: `slow` (tortoise) and `fast` (hare), both pointing to the head initially.
3. Move the `slow` pointer one step at a time, and the `fast` pointer two steps at a time.
4. If there is a cycle, the `fast` pointer will eventually meet the `slow` pointer.
5. If the `fast` pointer reaches the end of the list (i.e., `fast.next` or `fast.next.next` is null), return false (no cycle).
6. If the `slow` and `fast` pointers meet, return true (cycle detected).

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
The time complexity is O(n) in the worst case (when there is no cycle), as the `slow` pointer will need to traverse the entire list. The space complexity is O(1) since we are using a constant amount of extra space (two pointers).

# Code
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null) return false;
        ListNode slow = head, fast = head;
        while(fast.next != null && fast.next.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast) return true;
        }
        return false;
    }
}
```