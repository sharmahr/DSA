[Product of Array and Sef](https://leetcode.com/problems/product-of-array-except-self/description/)

# Intuition
The problem asks for an array where each element at index i is the product of all the elements in the original array except the element at index i. The intuitive approach is to calculate the product of all the elements to the left of each index and the product of all the elements to the right of each index, and then multiply these two values to get the desired result.

# Approach
1. Initialize two arrays, `pre` and `suff`, of length n (same as the input array `nums`).
2. Set `pre[0]` and `suff[n-1]` to 1 as the product of elements to the left of the first element and to the right of the last element is 1.
3. Iterate from left to right, starting from index 1 to n-1, and calculate the prefix product for each index i as `pre[i] = pre[i-1] * nums[i-1]`. This stores the product of all elements to the left of index i.
4. Iterate from right to left, starting from index n-2 to 0, and calculate the suffix product for each index i as `suff[i] = suff[i+1] * nums[i+1]`. This stores the product of all elements to the right of index i.
5. Create a result array `ans` of length n.
6. Iterate from 0 to n-1, and for each index i, calculate `ans[i] = pre[i] * suff[i]`, which gives the product of all elements except the element at index i.
7. Return the `ans` array.

# Complexity
- Time complexity: O(n), where n is the length of the input array `nums`. We iterate through the array three times: once to calculate the prefix products, once to calculate the suffix products, and once to calculate the final result.
- Space complexity: O(n), as we use two additional arrays, `pre` and `suff`, of length n to store the prefix and suffix products, and a result array `ans` of length n.

# Code
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int pre[] = new int[n];
        int suff[] = new int[n];
        pre[0] = 1;
        suff[n - 1] = 1;
        
        for(int i = 1; i < n; i++) {
            pre[i] = pre[i - 1] * nums[i - 1];
        }
        for(int i = n - 2; i >= 0; i--) {
            suff[i] = suff[i + 1] * nums[i + 1];
        }
        
        int ans[] = new int[n];
        for(int i = 0; i < n; i++) {
            ans[i] = pre[i] * suff[i];
        }
        return ans;
    }
}
```