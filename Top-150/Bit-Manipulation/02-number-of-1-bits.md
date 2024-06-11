[Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

# Intuition
The problem is to count the number of '1' bits in the binary representation of an integer. The intuitive approach is to perform a bitwise AND operation between the number and its predecessor, which will effectively turn off the rightmost '1' bit in each iteration. By counting the number of iterations required to reduce the number to zero, we can determine the count of '1' bits.

# Approach
1. Initialize a variable `count` to keep track of the number of '1' bits.
2. Start a loop that continues as long as `n` is greater than zero.
3. Inside the loop, perform a bitwise AND operation between `n` and `n-1`. This operation will turn off the rightmost '1' bit in `n`.
4. Increment the `count` variable by 1 to account for the '1' bit that was turned off.
5. Repeat steps 3-4 until `n` becomes zero.
6. Return the final value of `count`, which represents the number of '1' bits in the original integer.

# Complexity
- Time complexity: $O(k)$, where $k$ is the number of '1' bits in the binary representation of the integer. In the worst case, when all bits are '1', the time complexity becomes $O(log(n))$, where $n$ is the input integer.
- Space complexity: $O(1)$ as the solution uses only a constant amount of extra space.

# Code
```java
class Solution {
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            n &= (n - 1);
            count++;
        }
        return count;
    }
}
```