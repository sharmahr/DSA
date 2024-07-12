[Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

# Intuition
The problem of generating all possible letter combinations for a given string of digits can be solved using a backtracking approach. The intuition is to build the combinations by appending one letter at a time from the corresponding digit's letters and recursively generating combinations for the remaining digits.

# Approach
1. If the input string `digits` is empty, return an empty list since there are no combinations.
2. Create a mapping array `map` where each index corresponds to a digit (0-9) and holds the corresponding letters for that digit.
3. Initialize an empty result list to store all the generated letter combinations.
4. Define a recursive function `backtrack` that takes the following parameters:
   - `combination`: The current letter combination being built.
   - `nextDigits`: The remaining digits to process.
   - `map`: The mapping array to get the letters for each digit.
   - `result`: The list to store all the generated letter combinations.
5. In the `backtrack` function:
   - Base case: If `nextDigits` is empty, add the current `combination` to the result list and return.
   - Get the letters corresponding to the first digit in `nextDigits` using the `map` array.
   - Iterate through each letter in the obtained letters:
     - Recursively call `backtrack` with the updated `combination` (appending the current letter) and the remaining digits (excluding the first digit).
6. Start the backtracking process by calling `backtrack` with an empty combination, the input `digits`, the `map` array, and the empty result list.
7. Return the result list containing all the generated letter combinations.

# Complexity
- Time complexity: $O(4^n)$, where $n$ is the length of the input string `digits`. In the worst case, when all digits correspond to the digit '7' or '9' (which have 4 letters each), the algorithm generates $4^n$ combinations.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is equal to the length of the input string `digits`.

# Code
```java
class Solution {
    public List<String> letterCombinations(String digits) {
        if(digits.isEmpty()) return Collections.emptyList();

        String[] map = {"abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        List<String> result = new ArrayList<>();
        backtrack("", digits, map, result);
        return result;
    }

    void backtrack(String combination, String nextDigits, String[] map, List<String> result){
        if(nextDigits.isEmpty()){
            result.add(combination);
        }else{
            String letters = map[nextDigits.charAt(0) - '2'];
            for(char letter: letters.toCharArray()){
                backtrack(combination + letter, nextDigits.substring(1), map, result);
            }
        }
    }
}
```