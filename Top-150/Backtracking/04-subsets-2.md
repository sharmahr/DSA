[Subset 2](https://leetcode.com/problems/subsets-ii/description/)


# Intuition
The problem of generating all unique subsets of a given set that may contain duplicates can be solved using a recursive approach similar to generating subsets without duplicates. The key difference is that we need to handle duplicates to avoid generating duplicate subsets. Sorting the input array helps in identifying and skipping duplicates during the subset generation process.

# Approach
1. Sort the input array `nums` to group duplicate elements together.
2. Initialize an empty result list to store all the generated unique subsets.
3. Define a recursive function `generateSubset` that takes the following parameters:
   - `nums`: The sorted input array.
   - `index`: The current index being considered.
   - `current`: The current subset being built.
   - `result`: The list to store all the generated unique subsets.
4. In the `generateSubset` function:
   - Add the current subset to the result list.
   - Iterate from the current index to the end of the array:
     - If the current element is a duplicate of the previous element (i.e., `nums[i] == nums[i - 1]`) and the current index is not the starting index, skip the current element to avoid generating duplicate subsets.
     - Include the current element by adding it to the current subset.
     - Recursively call `generateSubset` with the next index to generate subsets including the current element.
     - Exclude the current element by removing it from the current subset (backtracking).
5. Start the recursive process by calling `generateSubset` with an empty current subset and index 0.
6. Return the result list containing all the generated unique subsets.

# Complexity
- Time complexity: $O(2^n)$, where n is the number of elements in the input array. This is because we generate all possible subsets, and there can be up to $2^n$ unique subsets.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is equal to the number of elements in the input array.

# Code
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // Sort the input array to handle duplicates
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        generateSubset(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private void generateSubset(int[] nums, int index, List<Integer> current, List<List<Integer>> result) {
        // Add the current subset to the result
        result.add(new ArrayList<>(current));
        
        // Generate subsets by including or excluding each element starting from index
        for (int i = index; i < nums.length; i++) {
            // Skip duplicates
            if (i > index && nums[i] == nums[i - 1]) {
                continue;
            }
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