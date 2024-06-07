[Problem Statement](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/description/)

# Intuition
The problem requires swapping the values of the kth node from the beginning and the kth node from the end of a singly-linked list. The intuition is to find these two nodes and then swap their values.

# Approach
1. Traverse the linked list to find the total number of nodes.
2. Calculate the position of the kth node from the end using the total number of nodes and k.
3. Traverse the linked list again to find the kth node from the beginning and the kth node from the end.
4. Swap the values of these two nodes.

# Complexity
- Time complexity:
$$O(n)$$, where n is the number of nodes in the linked list. We need to traverse the linked list twice to find the total number of nodes and the kth nodes.

- Space complexity:
$$O(1)$$ as we only use a constant amount of extra space to store pointers and variables.

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
    public ListNode swapNodes(ListNode head, int k) {
        // Find the total number of nodes
        int n = 0;
        ListNode current = head;
        while (current != null) {
            n++;
            current = current.next;
        }
        
        // Find the kth node from the beginning
        ListNode kthFromStart = head;
        for (int i = 1; i < k; i++) {
            kthFromStart = kthFromStart.next;
        }
        
        // Find the kth node from the end
        ListNode kthFromEnd = head;
        for (int i = 0; i < n - k; i++) {
            kthFromEnd = kthFromEnd.next;
        }
        
        // Swap the values of the kth nodes
        int temp = kthFromStart.val;
        kthFromStart.val = kthFromEnd.val;
        kthFromEnd.val = temp;
        
        return head;
    }
}
```

The code finds the total number of nodes in the linked list by traversing it once. Then, it finds the kth node from the beginning by moving a pointer k-1 steps forward from the head. To find the kth node from the end, it moves a pointer n-k steps forward from the head. Finally, it swaps the values of these two nodes and returns the head of the modified linked list.