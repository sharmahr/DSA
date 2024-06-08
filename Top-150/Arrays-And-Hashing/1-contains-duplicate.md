[Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

# Intuition
The intuition behind this solution is to use the input array itself as a hash table to keep track of the elements we have encountered so far. By negating the value at the index corresponding to each element, we can mark it as visited. If we encounter a negative value at an index, it means we have already visited that element before, indicating a duplicate.

To remember this solution, think of using the input array as a hash table and negating the values to mark elements as visited.

# Approach
1. Iterate through each element in the input array `nums`.
2. For each element `nums[i]`, calculate its absolute value `index = Math.abs(nums[i])`.
3. Check if `nums[index]` is negative:
   - If it is negative, it means we have already encountered the element at index `index` before, indicating a duplicate. Return `true`.
   - If it is positive, negate `nums[index]` to mark it as visited.
4. If we complete the iteration without finding any duplicates, return `false`.

# Complexity
- Time complexity: $O(n)$, where $n$ is the length of the input array `nums`. We iterate through the array once.
- Space complexity: $O(1)$. We use the input array itself as a hash table, so no additional space is required.

# Code
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            int index = Math.abs(nums[i]);
            if (nums[index] < 0) {
                return true; // We found a duplicate
            } else {
                nums[index] = -nums[index]; // Mark the element as visited
            }
        }
        return false; // No duplicate found
    }
}
```