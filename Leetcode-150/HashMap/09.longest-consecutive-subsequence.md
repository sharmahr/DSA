[Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

# Intuition
The problem asks us to find the length of the longest consecutive sequence in an unsorted array of integers. The intuitive approach is to use a hash set to store all the numbers in the array and then iterate through the set to find the longest consecutive sequence. By using a hash set, we can achieve O(1) lookup time for each number.

# Approach
1. Create an empty hash set called `hashset`.
2. Iterate through each number `i` in the input array `nums` and add it to the `hashset`.
3. Initialize a variable `length` to keep track of the length of the longest consecutive sequence.
4. Iterate through each number `x` in the `hashset`.
   - If `x-1` is not present in the `hashset`, it means `x` is the start of a potential consecutive sequence.
     - Initialize a variable `y` to `x+1`.
     - While `y` is present in the `hashset`, keep incrementing `y` to find the end of the consecutive sequence.
     - Update `length` with the maximum value between the current `length` and the length of the consecutive sequence `y-x`.
5. Return the value of `length`, which represents the length of the longest consecutive sequence.

# Complexity
- Time complexity: O(n), where n is the number of elements in the input array `nums`. Adding all the numbers to the hash set takes O(n) time, and iterating through the hash set to find the longest consecutive sequence also takes O(n) time in the worst case.
- Space complexity: O(n), where n is the number of elements in the input array `nums`. In the worst case, all the numbers in the array are unique and will be stored in the hash set.

# Code
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> hashset = new HashSet<>();

        for (int i: nums){
            hashset.add(i);
        }
        int length = 0;
        for (int x:hashset){
            if(!hashset.contains(x-1)){
                int y = x+1;
                while(hashset.contains(y)){
                    y++;
                }
                length= Math.max(length,y-x);
            }
        }
        return length;
    }
}
```