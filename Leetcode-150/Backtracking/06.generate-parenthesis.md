[Generate Parenthesis](https://leetcode.com/problems/generate-parentheses/description/)

# Intuition
The problem is to generate all possible combinations of well-formed parentheses, given a number `n` that represents the number of pairs of parentheses. The intuition is to use a recursive backtracking approach to generate the combinations.

The key idea is to ensure that at any point in the recursion, the number of closing parentheses does not exceed the number of opening parentheses. This property ensures that the generated combinations are well-formed.

# Approach
1. Define a recursive helper function `generate(s, open, close, result)` that takes the following parameters:
   - `s`: the current combination of parentheses
   - `open`: the remaining number of opening parentheses to be added
   - `close`: the remaining number of closing parentheses to be added
   - `result`: a list to store the final valid combinations
2. In the `generate` function:
   a. Base case: If both `open` and `close` are 0, it means a valid combination has been formed. Add `s` to the `result` list and return.
   b. If `open` is greater than 0, recursively call `generate` with `s + "(", open - 1, close, result)` to add an opening parenthesis.
   c. If `close` is greater than `open`, recursively call `generate` with `s + ")", open, close - 1, result)` to add a closing parenthesis.
3. In the main function `generateParenthesis`:
   a. Initialize an empty list `result` to store the valid combinations.
   b. Call the helper function `generate("", n, n, result)` with an empty string, `n` opening parentheses, and `n` closing parentheses.
   c. Return the `result` list containing all valid combinations.

# Complexity
- Time complexity: O(2^n)
* Space complexity: O(n)
The time complexity is O(2^n) because we need to generate all possible combinations, and there are 2^n possible combinations of parentheses for a given `n`. The space complexity is O(n) because, in the worst case, the recursion stack will have a depth of n when generating a combination with all opening parentheses first, followed by all closing parentheses.

# Code
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        generate("", n, n, result);
        return result;
    }

    private void generate(String s, int open, int close, List<String> result) {
        // Base case: If both open and close parentheses are used up
        if (open == 0 && close == 0) {
            result.add(s);
            return;
        }

        // Recursively generate combinations
        if (open > 0) {
            generate(s + "(", open - 1, close, result);
        }
        if (close > open) {
            generate(s + ")", open, close - 1, result);
        }
    }
}
```