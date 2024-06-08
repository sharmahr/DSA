[Find the duplicate number](https://leetcode.com/problems/find-the-duplicate-number/description/)

# Intuition
The problem is to find the duplicate number in an array of integers, where each number is in the range [1, n] and there is exactly one duplicate. The constraint is to solve the problem without modifying the array and using only constant extra space. The intuition is to use the concept of linked lists to treat the array as a linked list with nodes pointing to the indices represented by their values.

# Approach
1. Create two pointers: `slow` and `fast`.
2. Move the `slow` pointer one step at a time, and the `fast` pointer two steps at a time, by treating the array as a linked list where `nums[i]` is the next node for index `i`.
3. If there is a cycle in the linked list (i.e., a duplicate number), the `slow` and `fast` pointers will eventually meet.
4. Once the `slow` and `fast` pointers meet, reset one of the pointers (e.g., `slow`) to the start of the linked list (index 0).
5. Move both pointers one step at a time until they meet again. The index where they meet is the duplicate number.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)
The time complexity is O(n) because we need to iterate through the array once to find the intersection point. The space complexity is O(1) since we are using only two pointers as extra space.

# Code
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];

        // Find the meeting point of slow and fast pointers
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        // Reset slow to the start of the list
        slow = nums[0];

        // Find the start of the cycle (the duplicate number)
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }
}
```