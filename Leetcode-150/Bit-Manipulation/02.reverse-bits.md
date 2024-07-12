[Reverse Bits](https://leetcode.com/problems/reverse-bits/)

# Intuition
To reverse the bits of a given 32-bit unsigned integer, we can iterate over each bit from the least significant bit to the most significant bit. In each iteration, we extract the last bit of the input number, add it to the result, and then shift the input number to the right by 1 to process the next bit.

# Approach
1. Initialize a variable `result` to store the reversed bits.
2. Iterate 32 times (since the input is a 32-bit integer) using a loop variable `i`.
3. In each iteration:
   - Extract the last bit of the input number `n` using the bitwise AND operation `n & 1`.
   - Add the extracted bit to the result by left-shifting `result` by 1 and performing a bitwise OR operation with the extracted bit.
   - Shift the input number `n` to the right by 1 to process the next bit in the next iteration.
4. After iterating 32 times, the `result` variable will contain the reversed bits of the input number.
5. Return the `result`.

# Complexity
- Time complexity: $O(1)$ since we iterate a fixed number of times (32) regardless of the input value.
- Space complexity: $O(1)$ as we only use a constant amount of extra space.

# Code
```java
public class Solution {
    public int reverseBits(int n) {
        int result = 0;
        for (int i = 0; i < 32; i++) {
            result = (result << 1) | (n & 1);
            n >>= 1;
        }
        return result;
    }
}
```