[Plus One](https://leetcode.com/problems/plus-one/description/)


# Intuition
The problem is to increment a large integer represented as an array of digits by one. The intuition is to start from the least significant digit (rightmost) and increment it by one. If the digit becomes 10, we need to set it to 0 and carry over the increment to the next digit. We repeat this process until we find a digit less than 9 or reach the most significant digit (leftmost).

# Approach
1. Start from the last digit (rightmost) of the array.
2. Increment the current digit by one.
3. If the incremented digit is less than 10, we can simply return the modified array as the result.
4. If the incremented digit becomes 10, set it to 0 and move to the next digit (towards the left).
5. Repeat steps 3-4 until we find a digit less than 9 or reach the leftmost digit.
6. If we have processed all the digits and still haven't returned, it means the entire array consists of 9's. In this case, we need to create a new array with one more digit, set the first digit to 1, and return the new array.

# Complexity
- Time complexity: $O(n)$, where $n$ is the length of the input array.
  - In the worst case, we need to iterate through all the digits once.
- Space complexity: $O(1)$ or $O(n)$
  - If the input array does not consist of all 9's, we modify the input array in-place, so the space complexity is $O(1)$.
  - If the input array consists of all 9's, we need to create a new array with one more digit, resulting in a space complexity of $O(n)$.

# Code
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        
        // Start from the last digit
        for (int i = n - 1; i >= 0; i--) {
            if (digits[i] < 9) {
                // If current digit is less than 9, simply increment and return
                digits[i]++;
                return digits;
            } else {
                // If current digit is 9, set it to 0 and carry over to the next digit
                digits[i] = 0;
            }
        }
        
        // If we are here, it means the entire digits array was [9, 9, ..., 9]
        // Create a new array with one more digit (leading 1 followed by all 0s)
        int[] result = new int[n + 1];
        result[0] = 1;
        return result;
    }
}
```