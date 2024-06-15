[Power x, n](https://leetcode.com/problems/powx-n/)

# Intuition
The problem is to implement the `pow(x, n)` function, which calculates `x` raised to the power `n`. The intuition is to use a recursive approach with a logarithmic time complexity by dividing the problem into subproblems of half the size. Instead of using the classic recursive approach `x * pow(x, n-1)`, we can use `pow(x*x, n/2)` to reduce the number of recursive calls.

# Approach
1. If `n` is equal to 0, return 1 since any number raised to the power 0 is 1.
2. If `n` is negative, we need to handle it separately:
   - If `n` is even, divide `n` by 2 and make it positive. Also, update `x` to be `(1/x) * (1/x)` to handle the case when `n` is `Integer.MIN_VALUE`.
   - If `n` is odd, make `n` positive and update `x` to be `1/x`.
3. If `n` is even, recursively call `myPow(x*x, n/2)` to calculate the result.
4. If `n` is odd, recursively call `myPow(x*x, n/2)` and multiply the result by `x`.

# Complexity
- Time complexity: $O(\log n)$
  - Each recursive call reduces the problem size by half, resulting in a logarithmic number of recursive calls.
- Space complexity: $O(\log n)$
  - The recursive calls occupy space on the call stack, and the maximum depth of recursion is logarithmic.

# Code
```java
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) {
            return 1;
        }
        // Make the negative values positive
        else if (n < 0) {
            // Whenever even, just divide it by 2
            // This will also include Integer.MIN_VALUE
            // We're doing this because if we do -n and n=Integer.MIN_VALUE,
            // it'll become a value greater than Integer.MAX_VALUE
            if (n % 2 == 0) {
                n = n / 2;
                n = -n;
                x = (1 / x) * (1 / x);
            } else {
                // Odds don't need to be divided as their negative is within the positive limit
                n = -n;
                x = 1 / x;
            }
        }
        if (n % 2 == 0) {
            // Even case
            return myPow(x * x, n / 2);
        } else {
            // Odd case
            return x * myPow(x * x, n / 2);
        }
    }
}
```