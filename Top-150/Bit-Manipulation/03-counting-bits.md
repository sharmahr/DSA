[Counting Bits](https://leetcode.com/problems/counting-bits/description/)

# Intuition
To solve this problem, we need to count the number of '1' bits in the binary representation of each number from 0 to n. The intuitive approach is to use the built-in `Integer.bitCount()` method in Java, which returns the number of one-bits in the two's complement binary representation of an integer.

# Approach
1. Create an integer array `result` of size `n+1` to store the counts of '1' bits for each number from 0 to n.
2. Iterate from 0 to n (inclusive) using a loop variable `i`.
3. For each number `i`, use the `Integer.bitCount()` method to count the number of '1' bits in its binary representation.
4. Store the count of '1' bits for each number `i` in the corresponding index of the `result` array.
5. Return the `result` array containing the counts of '1' bits for each number from 0 to n.

# Complexity
- Time complexity: $O(n)$, where $n$ is the input number. We iterate from 0 to n, and for each number, the `Integer.bitCount()` method takes constant time to count the number of '1' bits.
- Space complexity: $O(n)$ to store the `result` array of size $n+1$.

# Code
```java
class Solution {
    public int[] countBits(int n) {
        int[] result = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            result[i] = Integer.bitCount(i);
        }
        return result;
    }
}
```