[Permutations](https://leetcode.com/problems/permutations/description/)

# Intuition
The problem of generating all permutations of a given array can be solved using a backtracking approach. The intuition is to build permutations by making choices at each step, and backtrack when a complete permutation is formed or when an element has already been used.

# Approach
1. Initialize an empty result list to store all the generated permutations.
2. Create a boolean array `used` to keep track of the elements that have been used in the current permutation.
3. Define a recursive function `backtrack` that takes the following parameters:
   - `nums`: The input array of numbers.
   - `currentPermutation`: The current permutation being built.
   - `used`: The boolean array to track used elements.
   - `result`: The list to store all the generated permutations.
4. In the `backtrack` function:
   - Base case: If the length of the current permutation equals the length of `nums`, a complete permutation is formed. Add the current permutation to the result list and return.
   - Iterate through each element in `nums`:
     - If the current element has already been used, skip it and continue to the next element.
     - Add the current element to the current permutation.
     - Mark the current element as used.
     - Recursively call `backtrack` to generate permutations with the updated current permutation.
     - Backtrack by removing the last added element from the current permutation.
     - Mark the current element as unused.
5. Start the backtracking process by calling `backtrack` with the initial parameters.
6. Return the result list containing all the generated permutations.

# Complexity
- Time complexity: $O(n!)$, where n is the length of the input array. There are n! possible permutations, and the algorithm generates each permutation.
- Space complexity: $O(n)$ for the recursive call stack and the `used` array. The maximum depth of recursion is equal to the length of the input array.

# Code
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        boolean[] used = new boolean[nums.length];
        backtrack(nums, new ArrayList<>(), used, result);
        return result;
    }

    void backtrack(int[] nums, ArrayList<Integer> currentPermutation, boolean[] used, List<List<Integer>> result){
        // base condition: if the current permutation length equals nums length add it to the result
        if(currentPermutation.size() == nums.length){
            result.add(new ArrayList<>(currentPermutation));
            return;
        }

        for(int i=0;i<nums.length;i++){
            if(used[i]) continue; // skip the element already used
            currentPermutation.add(nums[i]);
            used[i] = true;

            backtrack(nums, currentPermutation, used, result);

            currentPermutation.remove(currentPermutation.size() - 1);
            used[i] = false;
        }
    }
}
```