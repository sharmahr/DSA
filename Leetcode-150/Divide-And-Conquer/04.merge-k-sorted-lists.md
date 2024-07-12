[Merge K sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

# Intuition
Instead of repeatedly merging pairs of linked lists, we can use a min-heap to efficiently find the node with the smallest value among all the linked lists and add it to the merged list. This way, we can merge all the linked lists in a single pass.

# Approach
1. Create a min-heap data structure (e.g., a priority queue) and add the head nodes of all non-empty linked lists to the heap.
2. Initialize a dummy node to serve as the starting point of the new merged list, and a `current` pointer to the dummy node.
3. While the heap is not empty:
   a. Remove the node with the smallest value from the heap (this will be the root of the min-heap).
   b. Append this node to the `current` node in the new list.
   c. If the removed node has a next node, add the next node to the heap.
   d. Move the `current` pointer forward in the new list.
4. Return the `next` node of the dummy node, which is the head of the new merged list.

# Complexity
- Time complexity: O(N log k)
* Space complexity: O(k)
The time complexity is O(N log k), where N is the total number of nodes in all linked lists, and k is the number of linked lists. This is because we need to add all N nodes to the min-heap and perform N operations to remove and add nodes to the heap. Each heap operation (insertion and removal) takes O(log k) time. The space complexity is O(k) because we need to store the head nodes of all k linked lists in the min-heap.

# Code
```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }

        PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> a.val - b.val);

        // Add the head nodes of all non-empty linked lists to the min-heap
        for (ListNode list : lists) {
            if (list != null) {
                minHeap.offer(list);
            }
        }

        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        // Merge the linked lists by repeatedly removing the node with the smallest value
        while (!minHeap.isEmpty()) {
            ListNode node = minHeap.poll();
            current.next = node;
            current = current.next;

            if (node.next != null) {
                minHeap.offer(node.next);
            }
        }

        return dummy.next;
    }
}
```