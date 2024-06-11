[Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)

# Intuition
To calculate the sum of two integers without using the '+' operator, we can utilize bitwise operations. The key idea is to use the XOR operation to calculate the sum without considering the carry, and then use the AND operation to calculate the carry. We repeat this process until there is no carry left.

# Approach
1. Initialize two variables, `a` and `b`, to store the input integers.
2. Start a loop that continues as long as `b` is not equal to zero.
3. Inside the loop:
   - Calculate the carry by performing a bitwise AND operation between `a` and `b`.
   - Calculate the sum without considering the carry by performing a bitwise XOR operation between `a` and `b`.
   - Left shift the carry by 1 position to align it with the next bit position.
4. Update `a` with the sum without carry and `b` with the left-shifted carry.
5. Repeat steps 3-4 until there is no carry left (i.e., `b` becomes zero).
6. Return the final value of `a`, which represents the sum of the input integers.

# Complexity
- Time complexity: $O(1)$ since the number of iterations is limited by the number of bits in the integers (32 bits for int).
- Space complexity: $O(1)$ as the solution uses only a constant amount of extra space.

# Code
```java
class Solution {
    public int getSum(int a, int b) {
        while (b != 0) {
            int carry = a & b;
            a = a ^ b;
            b = carry << 1;
        }
        return a;
    }
}
```