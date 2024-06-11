[Missing Number](https://leetcode.com/problems/missing-number/)

# Intuition
To find the missing number in the given array, we can utilize the fact that the array contains all numbers from 0 to n except for one missing number. By calculating the expected sum of all numbers from 0 to n and subtracting the actual sum of the numbers in the array, we can determine the missing number.

# Approach
1. Calculate the expected sum of all numbers from 0 to n using the formula: `expectedSum = n * (n + 1) / 2`.
2. Initialize a variable `actualSum` to store the sum of the numbers in the given array.
3. Iterate through the array and add each number to `actualSum`.
4. Subtract `actualSum` from `expectedSum` to obtain the missing number.
5. Return the missing number.

# Complexity
- Time complexity: $O(n)$, where $n$ is the length of the input array. We iterate through the array once to calculate the actual sum.
- Space complexity: $O(1)$ as we only use a constant amount of extra space.

# Code
```java
class Solution {
    public int missingNumber(int[] nums) {
        int n = nums.length;
        int expectedSum = n * (n + 1) / 2;
        int actualSum = 0;
        
        for (int num : nums) {
            actualSum += num;
        }
        
        return expectedSum - actualSum;
    }
}
```