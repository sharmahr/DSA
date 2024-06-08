[Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)

# Intuition
The problem is to add two non-negative numbers represented as linked lists, where each node contains a single digit, and the digits are stored in reverse order. The intuition is to perform digit-wise addition, similar to how we add numbers on paper, and propagate the carry to the next digit.

# Approach
1. Initialize a dummy node to serve as the starting point of the new linked list that will store the sum.
2. Initialize a carry variable to keep track of the carry from the previous digit addition.
3. Traverse both input linked lists simultaneously, adding the corresponding digits and the carry from the previous addition.
4. Store the units digit of the sum in the current node of the new linked list and propagate the carry to the next digit.
5. After traversing both input lists, handle any remaining carry by appending a new node to the end of the new linked list.
6. Return the `next` node of the dummy node, which will be the head of the new linked list representing the sum.

# Complexity
- Time complexity: O(max(m, n))
* Space complexity: O(max(m, n) + 1)
The time complexity is O(max(m, n)), where m and n are the lengths of the input linked lists, as we need to traverse the longer of the two lists. The space complexity is O(max(m, n) + 1) because we need to create a new linked list with at most `max(m, n) + 1` nodes in case of a carry at the end.

# Code
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;

        ListNode result = new ListNode(-1);
        ListNode current = result;
        int carry = 0;
        int sum = 0;
        while(l1 != null && l2 != null){
            sum = l1.val + l2.val + carry;
            carry = sum/10;
            current.next = new ListNode(sum % 10);
            current = current.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        while(l1 != null){
            sum = l1.val + carry;
            carry = sum/10;
            current.next = new ListNode(sum % 10);
            current = current.next;
            l1 = l1.next;
        }
        while(l2 != null){
            sum = l2.val + carry;
            carry = sum/10;
            current.next = new ListNode(sum % 10);
            current = current.next;
            l2 = l2.next;
        }

        if(carry != 0){
            current.next = new ListNode(carry);
        }
        return result.next;
    }
}
```