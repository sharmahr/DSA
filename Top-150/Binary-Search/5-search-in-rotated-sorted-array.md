[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

# Intuition
The given code implements a binary search algorithm to find the index of a target element in a rotated sorted array. The key intuition is to identify which half of the array is sorted and determine if the target element lies within that sorted half. By comparing the middle element with the target and the endpoints of the current search range, we can recursively narrow down the search space until the target is found or the search range is exhausted.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the start and end of the array, respectively.
2. While `left` is less than or equal to `right`, do the following:
   - Calculate the middle index `mid` using the formula `left + (right - left) / 2`.
   - If the middle element `nums[mid]` is equal to the target, return `mid` as the target is found.
   - If the left half of the array is sorted (i.e., `nums[left] <= nums[mid]`):
     - If the target lies within the range `[nums[left], nums[mid])`, update `right = mid - 1` to search in the left half.
     - Otherwise, update `left = mid + 1` to search in the right half.
   - If the right half of the array is sorted:
     - If the target lies within the range `(nums[mid], nums[right]]`, update `left = mid + 1` to search in the right half.
     - Otherwise, update `right = mid - 1` to search in the left half.
3. If the target is not found after the while loop ends, return -1 to indicate that the target is not present in the array.

# Complexity
- Time complexity: $O(\log n)$
The binary search algorithm has a logarithmic time complexity as it repeatedly divides the search space in half until the target is found or the search space is exhausted.

* Space complexity: $O(1)$
The algorithm uses only a constant amount of extra space for the `left`, `right`, and `mid` variables, regardless of the input size.

# Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            // If the left half is sorted
            if (nums[left] <= nums[mid]) {
                // Check if the target is in the left half
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            // If the right half is sorted
            else {
                // Check if the target is in the right half
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
}
```