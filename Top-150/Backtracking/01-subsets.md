[01-subsets](https://leetcode.com/problems/subsets/description/)

# Intuition
The problem of generating all subsets of a given set can be solved using a recursive approach. The intuition is to generate subsets by either including or excluding each element of the set. We can start with an empty subset and gradually build subsets by making decisions for each element.

# Approach
1. Initialize an empty result list to store all the generated subsets.
2. Define a recursive function `generateSubset` that takes the following parameters:
   - `nums`: The input array representing the set.
   - `index`: The current index being considered.
   - `current`: The current subset being built.
   - `result`: The list to store all the generated subsets.
3. In the `generateSubset` function:
   - Add the current subset to the result list.
   - Iterate from the current index to the end of the array:
     - Include the current element by adding it to the current subset.
     - Recursively call `generateSubset` with the next index to generate subsets including the current element.
     - Exclude the current element by removing it from the current subset (backtracking).
4. Start the recursive process by calling `generateSubset` with an empty current subset and index 0.
5. Return the result list containing all the generated subsets.

# Complexity
- Time complexity: $O(2^n)$, where n is the number of elements in the input array. This is because we generate all possible subsets, and there are $2^n$ subsets for a set of size n.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is equal to the number of elements in the input array.

# Code
```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        generateSubset(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void generateSubset(int[] nums, int index, List<Integer> current, List<List<Integer>> result) {
        // Add the current subset to the result
        result.add(new ArrayList<>(current));
        
        // Generate subsets by including or excluding each element starting from index
        for (int i = index; i < nums.length; i++) {
            // Include the current element
            current.add(nums[i]);
            // Recursively generate subsets starting from the next index
            generateSubset(nums, i + 1, current, result);
            // Exclude the current element to backtrack
            current.remove(current.size() - 1);
        }
    }
}
```