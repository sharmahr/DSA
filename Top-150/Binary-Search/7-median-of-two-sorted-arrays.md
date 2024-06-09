[Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

# Intuition
To find the median of two sorted arrays with a time complexity of O(log(m+n)), we can use the idea of binary search. Instead of merging the arrays and finding the median, we can perform a binary search on the smaller array to find the partition point that divides both arrays into left and right halves such that the elements in the left half are smaller than or equal to the elements in the right half. Once we find the correct partition, we can determine the median based on the maximum element in the left half and the minimum element in the right half.

# Approach
1. Ensure that `nums1` is the smaller array by comparing the lengths and swapping them if necessary.
2. Initialize variables `m` and `n` as the lengths of `nums1` and `nums2`, respectively, and `leftHalfLength` as the length of the left half of the combined array.
3. Perform a binary search on the smaller array `nums1` to find the partition point.
4. In each iteration of the binary search:
   - Calculate the partition indices `partitionX` and `partitionY` for `nums1` and `nums2`, respectively.
   - Determine the maximum element on the left side (`maxLeftX` and `maxLeftY`) and the minimum element on the right side (`minRightX` and `minRightY`) for both arrays, handling edge cases when the partition is at the beginning or end of an array.
   - Check if `maxLeftX <= minRightY` and `maxLeftY <= minRightX`. If true, the correct partition is found.
     - If the combined array has an even length, the median is the average of the maximum of the left sides and the minimum of the right sides.
     - If the combined array has an odd length, the median is the maximum of the left sides.
   - If `maxLeftX > minRightY`, adjust the partition towards the left by updating `right` to `partitionX - 1`.
   - If `maxLeftY > minRightX`, adjust the partition towards the right by updating `left` to `partitionX + 1`.
5. If the binary search completes without finding the correct partition, throw an `IllegalArgumentException` indicating that the input arrays are not sorted.

# Complexity
- Time complexity: $O(\log(\min(m, n)))$
The binary search is performed on the smaller array, so the time complexity is logarithmic in the length of the smaller array. Since we ensure that `nums1` is the smaller array, the time complexity is $O(\log(\min(m, n)))$, where $m$ and $n$ are the lengths of `nums1` and `nums2`, respectively.

* Space complexity: $O(1)$
The algorithm uses only a constant amount of extra space for the variables used in the binary search and the calculations of the median. The space complexity is $O(1)$.

# Code
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        // Ensure nums1 is the smaller array
        if (nums1.length > nums2.length) {
            return findMedianSortedArrays(nums2, nums1);
        }
        
        int m = nums1.length;
        int n = nums2.length;
        int leftHalfLength = (m + n + 1) / 2;
        
        // Binary search on the smaller array nums1
        int left = 0;
        int right = m;
        
        while (left <= right) {
            int partitionX = left + (right - left) / 2;
            int partitionY = leftHalfLength - partitionX;
            
            int maxLeftX = (partitionX == 0) ? Integer.MIN_VALUE : nums1[partitionX - 1];
            int minRightX = (partitionX == m) ? Integer.MAX_VALUE : nums1[partitionX];
            int maxLeftY = (partitionY == 0) ? Integer.MIN_VALUE : nums2[partitionY - 1];
            int minRightY = (partitionY == n) ? Integer.MAX_VALUE : nums2[partitionY];
            
            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                // Found the correct partition
                if ((m + n) % 2 == 0) {
                    // If the combined array has even length
                    return (Math.max(maxLeftX, maxLeftY) + Math.min(minRightX, minRightY)) / 2.0;
                } else {
                    // If the combined array has odd length
                    return Math.max(maxLeftX, maxLeftY);
                }
            } else if (maxLeftX > minRightY) {
                // Adjust the partition towards the left
                right = partitionX - 1;
            } else {
                // Adjust the partition towards the right
                left = partitionX + 1;
            }
        }
        
        return 0.0;
    }
}
```