[Merge Two Sorted List](https://leetcode.com/problems/merge-two-sorted-lists/description/)

# Intuition
The problem is to merge two sorted linked lists into a new sorted linked list. The intuition is to compare the values of the nodes in the two input lists and add the smaller value node to the new list, while moving the pointer in the corresponding input list forward.

# Approach
1. Create a dummy node to serve as the starting point of the new merged list.
2. Initialize a `current` pointer to the dummy node.
3. Iterate through both input lists `list1` and `list2` while they are not null:
   a. Compare the values of the current nodes in `list1` and `list2`.
   b. Append the node with the smaller value to the `current` node in the new list.
   c. Move the pointer of the corresponding input list forward.
   d. Move the `current` pointer forward in the new list.
4. After the loop, one of the input lists may have remaining nodes. Append the remaining nodes to the end of the new list.
5. Return the `next` node of the dummy node, which is the head of the new merged list.

# Complexity
- Time complexity: O(n + m)
* Space complexity: O(1)
The time complexity is O(n + m), where n and m are the lengths of the two input lists, as we need to iterate through both lists. The space complexity is O(1) since we are using a constant amount of extra space (a few pointers), regardless of the size of the input.

# Code
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(-1); // starting node of the list
        ListNode current = dummy;
        while(list1 != null && list2 != null){
            if(list1.val < list2.val){
                current.next = list1;
                list1 = list1.next;
            }else{
                current.next = list2;
                list2 = list2.next;
            }
            current = current.next;
        }

        if(list1 != null){
            current.next = list1;
        }else{
            current.next = list2;
        }

        return dummy.next; // because the first node will contain -1
    }
}
```