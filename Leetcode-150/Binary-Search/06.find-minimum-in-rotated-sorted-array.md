[Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

# Intuition
The problem can be solved using a modified binary search approach. Since the array is sorted in ascending order, the key idea is to find the pivot point where the value transitions from a larger value to a smaller value. This pivot point is the minimum value in the rotated sorted array.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the start and end of the array, respectively.
2. While `left` is less than `right`, perform the following steps:
   a. Calculate the middle index `mid` using `left + (right - left) / 2`.
   b. If the element at `mid` is less than the element at `right`, it means the minimum value lies between `left` and `mid`. Update `right` to `mid`.
   c. Otherwise, the minimum value lies between `mid + 1` and `right`. Update `left` to `mid + 1`.
3. After the loop terminates, `left` will point to the minimum value in the rotated sorted array.

# Complexity
- Time complexity: O(log n), where n is the length of the input array. This is because the algorithm performs a modified binary search, which has a time complexity of O(log n).
- Space complexity: O(1), since the algorithm uses a constant amount of extra space.

# Code
```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0, right = nums.length - 1;
        while(left < right) {
            int mid = left + (right - left) / 2;

            if(nums[mid] < nums[right]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return nums[left];
    }
}
```