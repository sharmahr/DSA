[Reverse a Linked List](https://leetcode.com/problems/reverse-linked-list/)

# Intuition
The problem is to reverse a singly linked list. The intuition is to iteratively update the next pointers of each node to point to the previous node, effectively reversing the direction of the list.

# Approach
1. Check if the head is null or if it has only one node. If so, return the head itself as it is already reversed.
2. Initialize three pointers: `prev` (to keep track of the previously reversed part), `current` (to keep track of the current node), and `temp` (to temporarily store the next node).
3. Iterate through the linked list:
   a. Store the next node in `temp`.
   b. Reverse the link of the current node by making its `next` pointer point to the previously reversed part (`prev`).
   c. Move `prev` and `current` pointers one step forward.
4. After the loop, `prev` will be pointing to the new head of the reversed linked list.
5. Return `prev`.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
The time complexity is O(n), where n is the number of nodes in the linked list, as we need to iterate through the entire list once. The space complexity is O(1) since we are using a constant amount of extra space (three pointers), regardless of the size of the input.

# Code
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        // reverse the linkedlist by iterative approach
        if(head == null || head.next == null) return head;

        ListNode prev = null, current = head;
        while(current != null){
            ListNode temp = current.next;
            current.next = prev;
            prev = current;
            current = temp;
        }
        return prev;
    }
}
```