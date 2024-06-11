[Reverse Integer](https://leetcode.com/problems/reverse-integer/description/)

# Intuition
To reverse an integer, we can repeatedly extract the last digit of the number and append it to the reversed result. We need to handle the case of integer overflow by checking if the reversed result exceeds the range of a 32-bit signed integer.

# Approach
1. Initialize a variable `reversed` to store the reversed integer. We use a `long` data type to handle larger values and avoid integer overflow during the reversal process.
2. Start a loop that continues as long as the input integer `x` is not equal to zero.
3. Inside the loop:
   - Extract the last digit of `x` by using the modulo operator `%` with 10 and add it to the `reversed` variable multiplied by 10.
   - Divide `x` by 10 to remove the last digit.
   - Check if the `reversed` variable exceeds the range of a 32-bit signed integer (i.e., `Integer.MAX_VALUE` or `Integer.MIN_VALUE`). If it does, return 0 to indicate an overflow.
4. Repeat steps 3-4 until `x` becomes zero.
5. Return the `reversed` variable cast to an `int` to fit within the range of a 32-bit signed integer.

# Complexity
- Time complexity: $O(\log x)$ since the number of iterations is proportional to the number of digits in the input integer `x`.
- Space complexity: $O(1)$ as the solution uses only a constant amount of extra space.

# Code
```java
class Solution {
    public int reverse(int x) {
        long reversed = 0;
        while (x != 0) {
            reversed = reversed * 10 + x % 10;
            x /= 10;
            if (reversed > Integer.MAX_VALUE || reversed < Integer.MIN_VALUE) {
                return 0;
            }
        }
        return (int) reversed;
    }
}
```