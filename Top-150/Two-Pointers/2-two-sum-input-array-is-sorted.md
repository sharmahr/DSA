[Two Sum Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

# Intuition
The problem asks to find two numbers in a sorted array whose sum is equal to a given target value. The intuition is to use the two-pointer approach, where we start with two pointers, one at the beginning and one at the end of the array, and move them based on the sum of the elements they point to.

# Approach
1. Initialize two pointers, `left` and `right`, pointing to the first and last indices of the array, respectively.
2. Since the array is sorted, we can optimize the initial position of the `right` pointer by moving it to the rightmost position where the element is less than or equal to the target value.
3. While `left` is less than `right`, do the following:
   a. Calculate the sum of the elements at `left` and `right`.
   b. If the sum is greater than the target, decrement `right` to reduce the sum.
   c. If the sum is less than the target, increment `left` to increase the sum.
   d. If the sum is equal to the target, return the indices (1-based) of the two elements.
4. If the loop completes without finding the solution, return `{0, 0}` as per the problem statement.

# Complexity
- Time complexity: O(n), where n is the length of the input array. In the worst case, we need to iterate through the entire array once.
- Space complexity: O(1), as we are using only a constant amount of extra space for the pointers and temporary variables.

# Code
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int right = numbers.length - 1;
        int left = 0;
        while(left < right){
            int sum = numbers[left] + numbers[right];
            if(sum > target){
                right -= 1;
            }else if(sum < target){
                left += 1;
            }else{
                return new int[]{left+1, right+1};
            }
        }
        
        return new int[]{0,0};
    }
}
```