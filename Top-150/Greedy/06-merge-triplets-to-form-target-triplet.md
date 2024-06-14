[Merge Triplets to form Target Triplets](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/)

# Intuition
The problem of determining if we can merge triplets to form a target triplet can be solved using a greedy approach. The intuition is to iterate through each triplet and update a new triplet with the maximum values from the current triplet and the previously merged triplet, as long as each value is less than or equal to the corresponding value in the target triplet. If the merged triplet matches the target triplet at the end, it means we can merge the triplets to form the target triplet.

# Approach
1. Initialize a new triplet array `triplet` with all values set to 0.
2. Iterate through each triplet in the `triplets` array:
   - Check if the maximum value of each element in the current triplet and the corresponding element in the `triplet` array is less than or equal to the corresponding value in the `target` triplet.
   - If the condition is satisfied, update each element in the `triplet` array with the maximum value between the current triplet and the `triplet` array.
3. After iterating through all triplets, check if the `triplet` array matches the `target` triplet. If they match, return true; otherwise, return false.

# Complexity
- Time complexity: O(n), where n is the number of triplets in the `triplets` array. We iterate through each triplet once.
- Space complexity: O(1) since we only use a constant amount of extra space for the `triplet` array.

# Code
```java
class Solution {
    public boolean mergeTriplets(int[][] triplets, int[] target) {
        int[] triplet = new int[3];
        for(int i=0;i<triplets.length;i++){
            if(Math.max(triplets[i][0], triplet[0]) <= target[0] 
                && Math.max(triplets[i][1], triplet[1]) <= target[1]
                && Math.max(triplets[i][2], triplet[2]) <= target[2]) {
                    
                    triplet[0] = Math.max(triplets[i][0], triplet[0]);
                    triplet[1] = Math.max(triplets[i][1], triplet[1]);
                    triplet[2] = Math.max(triplets[i][2], triplet[2]);
            }
        }

        if(triplet[0] == target[0] && triplet[1] == target[1] && triplet[2] == target[2]) return true;
        return false;
    }
}
```