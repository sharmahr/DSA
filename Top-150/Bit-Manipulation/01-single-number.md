[Single Number](https://leetcode.com/problems/single-number/)

# Intuition
The problem asks to find the single number that appears only once in the array, while all other numbers appear twice. The intuition is to use the XOR operation, which has the following properties:
- XORing a number with itself results in 0.
- XORing a number with 0 results in the number itself.
- XORing is associative and commutative.

By XORing all the numbers in the array, the duplicate numbers will cancel out each other, leaving only the single number.

# Approach
1. Initialize a variable `result` to store the XOR of all numbers.
2. Iterate through the array and XOR each number with `result`.
3. After the iteration, `result` will hold the single number that appears only once.
4. Return `result`.

# Complexity
- Time complexity: O(n)
  - The solution iterates through the array once, where n is the size of the array.
- Space complexity: O(1)
  - The solution uses only a constant amount of extra space for the `result` variable.

# Code
```java
class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }
        return result;
    }
}
```