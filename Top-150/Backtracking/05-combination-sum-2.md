[Combination Sum 2](https://leetcode.com/problems/combination-sum-ii/description/)

# Intuition
The problem of finding all unique combinations that sum up to a target, where each candidate can be used only once, can be solved using a backtracking approach similar to the combination sum problem. The key difference is that we need to handle duplicates and ensure that each candidate is used at most once in each combination. Sorting the input array helps in identifying and skipping duplicates during the backtracking process.

# Approach
1. Sort the input array `candidates` to group duplicate elements together.
2. Initialize an empty result list to store all the unique combinations.
3. Define a recursive function `backtrack` that takes the following parameters:
   - `candidates`: The sorted input array of candidate numbers.
   - `target`: The remaining target sum to be achieved.
   - `start`: The starting index to consider candidates from.
   - `currentCombination`: The current combination being built.
   - `result`: The list to store all the unique combinations.
4. In the `backtrack` function:
   - Base case: If target is 0, a valid combination is found. Add the current combination to the result list and return.
   - Iterate through the candidates array starting from the `start` index:
     - If the current candidate is a duplicate of the previous candidate (i.e., `candidates[i] == candidates[i - 1]`) and the current index is not the starting index, skip the current candidate to avoid generating duplicate combinations.
     - If the current candidate is greater than the target, break the loop since the candidates are sorted in ascending order.
     - Add the current candidate to the current combination.
     - Recursively call `backtrack` with the updated target (subtracting the current candidate) and the next index (i + 1) to ensure each candidate is used at most once.
     - Backtrack by removing the last added candidate from the current combination.
5. Start the backtracking process by calling `backtrack` with the initial parameters.
6. Return the result list containing all the unique combinations.

# Complexity
- Time complexity: $O(2^n)$, where n is the total number of candidates. In the worst case, when the target is large and candidates are small, the algorithm explores all possible combinations, resulting in exponential time complexity.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is determined by the number of candidates and the target sum.

# Code
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }

    void backtrack(int[] candidates, int target, int start, ArrayList<Integer> currentCombination, List<List<Integer>> result){
        if(target == 0){
            result.add(new ArrayList<>(currentCombination));
            return;
        }

        for(int i=start; i < candidates.length; i++){
            //skip duplicates
            if( i > start && candidates[i] == candidates[i - 1]){
                continue;
            }
            if(candidates[i] > target) break;
            currentCombination.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i + 1, currentCombination, result);
            currentCombination.remove(currentCombination.size() - 1);
        }
    }
}
```