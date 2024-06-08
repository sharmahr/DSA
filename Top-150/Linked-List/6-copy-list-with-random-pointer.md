[Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

# Intuition
The problem is to create a deep copy of a linked list where each node has a `random` pointer that can point to any node in the list, including itself. The intuition is to use a dictionary (HashMap) to map the original nodes to their corresponding copied nodes. We can then iterate through the original list, create copies of the nodes, and update the `next` and `random` pointers of the copied nodes based on the original nodes and the dictionary.

# Approach
1. Create a dictionary `map` to store the mapping between the original nodes and their corresponding copied nodes.
2. Iterate through the original list and create a new node for each original node. Store the mapping between the original node and the new node in the `map`.
3. Iterate through the original list again, and for each node:
   a. Update the `next` pointer of the copied node based on the `next` pointer of the original node and the `map`.
   b. Update the `random` pointer of the copied node based on the `random` pointer of the original node and the `map`.
4. Return the `next` pointer of the first copied node, which will be the head of the copied linked list.

# Complexity
- Time complexity: O(n)
* Space complexity: O(n)
The time complexity is O(n), where n is the number of nodes in the linked list, as we need to iterate through the list twice. The space complexity is O(n) due to the use of the dictionary to store the mapping between original and copied nodes.

# Code
```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }

        Map<Node, Node> map = new HashMap<>();
        Node curr = head;

        // Create copies of the nodes and store the mapping
        while (curr != null) {
            map.put(curr, new Node(curr.val));
            curr = curr.next;
        }

        curr = head;

        // Update the next and random pointers of the copied nodes
        while (curr != null) {
            map.get(curr).next = map.get(curr.next);
            map.get(curr).random = map.get(curr.random);
            curr = curr.next;
        }

        return map.get(head);
    }
}
```