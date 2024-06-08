[3Sum](https://leetcode.com/problems/3sum/description/)

# Intuition
<!-- Describe your first thoughts on how to solve this problem and a note to remember the solution -->
The problem asks to find all unique triplets in a given array that sum up to zero. The intuition is to extend the two-pointer approach used in the two-sum problem to solve this problem. We can first sort the array, and then fix one element at a time. For each fixed element, we can use the two-pointer technique to find the other two elements that sum up to the negative of the fixed element.

# Approach
1. Sort the input array in ascending order.
2. Iterate through the array with a pointer `i`.
   a. Skip duplicates of the current element to avoid redundant triplets.
   b. For the current element `nums[i]`, use two pointers `j` and `k`, where `j` starts from `i+1` and `k` starts from the end of the array.
   c. While `j < k`, calculate the sum of `nums[i]`, `nums[j]`, and `nums[k]`.
      - If the sum is less than 0, increment `j` to increase the sum.
      - If the sum is greater than 0, decrement `k` to decrease the sum.
      - If the sum is 0, add the triplet `[nums[i], nums[j], nums[k]]` to the result list. Then, move both `j` and `k` inwards while skipping duplicates to avoid redundant triplets.
3. Return the result list containing all unique triplets that sum up to 0.

# Complexity
- Time complexity: O(n^2), where n is the length of the input array. In the worst case, we need to iterate through the sorted array once, and for each element, we perform the two-pointer approach, which takes O(n) time complexity.
- Space complexity: O(1), as we are using only a constant amount of extra space for pointers and temporary variables. The space required for the result list is not considered as part of the space complexity analysis.

# Code
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // sort the array

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i-1]) {
                continue;
            }
            
            int j = i + 1;
            int k = nums.length - 1;
            // follow two sum approach
            while (j < k) {
                int total = nums[i] + nums[j] + nums[k];

                if (total > 0) {
                    k--;
                } else if (total < 0) {
                    j++;
                } else {
                    result.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;

                    while (nums[j] == nums[j-1] && j < k) {
                        j++;
                    }
                }
            }
        }
        return result;        
    }
}
```