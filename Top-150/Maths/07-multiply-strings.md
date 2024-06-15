[Mutiply Strings](https://leetcode.com/problems/multiply-strings/description/)

# Intuition
The problem is to multiply two numbers represented as strings and return the result as a string. The intuition is to perform the multiplication digit by digit, similar to the traditional multiplication algorithm, and then reverse the result to get the final answer.

# Approach
1. Check if either `num1` or `num2` is "0". If so, return "0" since multiplying any number by 0 gives 0.
2. Create an integer array `res` to store the intermediate results. The length of `res` is set to the sum of the lengths of `num1` and `num2`.
3. Reverse both `num1` and `num2` using the `reverseString` helper function to simplify the multiplication process.
4. Iterate through each digit of `num1` and `num2` using nested loops:
   - Multiply the current digits of `num1` and `num2` to get the `digit` value.
   - Add the `digit` value to `res[i + j]`, where `i` and `j` are the indices of the current digits.
   - Add the carry (`res[i + j] / 10`) to `res[i + j + 1]`.
   - Update `res[i + j]` to store only the ones digit (`res[i + j] % 10`).
5. Reverse the `res` array using the `reverseArrayInPlace` helper function to get the correct order of digits.
6. Find the proper starting index `startIndex` in `res` to avoid leading zeros.
7. Construct the final result string by appending the digits from `startIndex` to the end of `res` using a `StringBuilder`.
8. Return the final result string.

# Complexity
- Time complexity: $O(m \times n)$, where $m$ and $n$ are the lengths of `num1` and `num2`, respectively.
  - The nested loops iterate through each digit of `num1` and `num2`, resulting in a total of $m \times n$ iterations.
- Space complexity: $O(m + n)$
  - The `res` array has a length of $m + n$ to store the intermediate results.
  - The `StringBuilder` used to construct the final result also takes $O(m + n)$ space.

# Code
```java
class Solution {
    public String multiply(String num1, String num2) {
        if ("0".equals(num1) || "0".equals(num2)) {
            return "0";
        }

        int[] res = new int[num1.length() + num2.length()];

        num1 = reverseString(num1);
        num2 = reverseString(num2);

        for (int i = 0; i < num1.length(); i++) {
            for (int j = 0; j < num2.length(); j++) {
                int digit =
                    Integer.valueOf(String.valueOf(num1.charAt(i))) *
                    Integer.valueOf(String.valueOf(num2.charAt(j)));
                res[i + j] += digit;
                res[i + j + 1] += res[i + j] / 10;
                res[i + j] = res[i + j] % 10;
            }
        }

        reverseArrayInPlace(res);

        // Get the proper starting point to avoid leading zeros
        int startIndex = 0;
        while (startIndex < res.length) {
            if (res[startIndex] != 0) {
                break;
            }
            startIndex++;
        }

        StringBuilder buildResponse = new StringBuilder();
        for (int i = startIndex; i < res.length; i++) {
            buildResponse.append(res[i]);
        }

        return buildResponse.toString();
    }

    private String reverseString(String str) {
        StringBuilder reversedStr = new StringBuilder(str);
        reversedStr.reverse();
        return reversedStr.toString();
    }

    private void reverseArrayInPlace(int[] arr) {
        for (int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - i - 1];
            arr[arr.length - i - 1] = temp;
        }
    }
}
```