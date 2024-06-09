[Binary Search](https://leetcode.com/problems/binary-search/description/)

# Intuition
The problem asks to find the index of a target element in a sorted array using the binary search algorithm. The intuition is to repeatedly divide the search interval in half by comparing the middle element with the target value. If the middle element is equal to the target, we have found the solution. If the target is greater than the middle element, we search in the right half of the interval. Otherwise, we search in the left half of the interval.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the start and end of the array, respectively.
2. While `left` is less than or equal to `right`, do the following:
   a. Calculate the middle index `mid` using `left + (right - left) / 2` to avoid integer overflow.
   b. If the element at `mid` is equal to the target, return `mid` as the index.
   c. If the target is greater than the element at `mid`, update `left` to `mid + 1` to search in the right half of the interval.
   d. Otherwise, update `right` to `mid - 1` to search in the left half of the interval.
3. If the loop completes without finding the target, return `-1` to indicate that the target is not present in the array.

# Complexity
- Time complexity: O(log n), where n is the length of the input array. In the worst case, we need to perform log n iterations to find the target or determine that it is not present in the array.
- Space complexity: O(1), as we are using only a constant amount of extra space for pointers and temporary variables.

# Code
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length -1;
        while(left <= right){
            int mid = left + (right - left)/2;
            if(nums[mid] == target) return mid;
            if(target>nums[mid]){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return -1;
    }
}
```