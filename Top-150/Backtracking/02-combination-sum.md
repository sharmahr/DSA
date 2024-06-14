[Combination Sum](https://leetcode.com/problems/combination-sum/)

# Intuition
The problem of finding all unique combinations that sum up to a target can be solved using a backtracking approach. The intuition is to generate combinations by making choices at each step, and backtrack when the sum exceeds the target or when a valid combination is found.

# Approach
1. Initialize an empty result list to store all the valid combinations.
2. Define a recursive function `backtrack` that takes the following parameters:
   - `candidates`: The input array of candidate numbers.
   - `remaining`: The remaining target sum to be achieved.
   - `start`: The starting index to consider candidates from.
   - `currentCombination`: The current combination being built.
   - `result`: The list to store all the valid combinations.
3. In the `backtrack` function:
   - Base case: If remaining is 0, a valid combination is found. Add the current combination to the result list and return.
   - If remaining is less than 0, the current combination is not valid. Return without proceeding further.
   - Iterate through the candidates array starting from the `start` index:
     - Add the current candidate to the current combination.
     - Recursively call `backtrack` with the updated remaining sum and the current index (to allow reusing the same candidate).
     - Backtrack by removing the last added candidate from the current combination.
4. Start the backtracking process by calling `backtrack` with the initial parameters.
5. Return the result list containing all the valid combinations.

# Complexity
- Time complexity: $O(2^n)$, where n is the total number of candidates. In the worst case, when the target is large and candidates are small, the algorithm explores all possible combinations, resulting in exponential time complexity.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is determined by the number of candidates and the target sum.

# Code
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int[] candidates, int remaining, int start, List<Integer> currentCombination, List<List<Integer>> result) {
        // Base case: if remaining is 0, we found a valid combination
        if (remaining == 0) {
            result.add(new ArrayList<>(currentCombination));
            return;
        }

        // If remaining is less than 0, no need to proceed further
        if (remaining < 0) {
            return;
        }

        // Try each candidate starting from the current position
        for (int i = start; i < candidates.length; i++) {
            currentCombination.add(candidates[i]);
            // Recursive call with the current candidate included
            backtrack(candidates, remaining - candidates[i], i, currentCombination, result);
            // Backtrack: remove the last added candidate
            currentCombination.remove(currentCombination.size() - 1);
        }
    }
}
```