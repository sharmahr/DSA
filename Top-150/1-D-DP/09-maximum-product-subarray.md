[Maximum Product SubArray](https://leetcode.com/problems/maximum-product-subarray/)

# Intuition
The problem of finding the maximum product subarray can be solved using dynamic programming. The intuition behind the solution is to keep track of both the maximum product and the minimum product encountered so far. This is because the minimum product can become the maximum product if multiplied by a negative number.

# Approach
We can solve this problem using a dynamic programming approach. We iterate through the array and maintain two variables: `maxProduct` and `minProduct`. At each step, we update these variables based on the current element.

1. If the current element is negative, we swap `maxProduct` and `minProduct` because the maximum product will become the minimum product when multiplied by a negative number, and vice versa.

2. We calculate the maximum product by multiplying the current element with the previous maximum product (`maxProduct`) or considering the current element alone. Similarly, we calculate the minimum product by multiplying the current element with the previous minimum product (`minProduct`) or considering the current element alone.

3. We update the overall maximum product (`result`) by taking the maximum of the current `result` and the current `maxProduct`.

4. We repeat steps 1-3 for all elements in the array.

# Complexity
- Time Complexity: $$O(n)$$, where n is the length of the input array. We iterate through the array once.
- Space Complexity: $$O(1)$$ as we only use a constant amount of extra space to store variables.

# Recursive Approach
```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        return maxProductHelper(nums, 0, nums.length - 1);
    }
    
    private int maxProductHelper(int[] nums, int left, int right) {
        if (left == right) {
            return nums[left];
        }
        
        int mid = left + (right - left) / 2;
        int leftMax = maxProductHelper(nums, left, mid);
        int rightMax = maxProductHelper(nums, mid + 1, right);
        int crossMax = maxCrossProduct(nums, left, mid, right);
        
        return Math.max(Math.max(leftMax, rightMax), crossMax);
    }
    
    private int maxCrossProduct(int[] nums, int left, int mid, int right) {
        int leftProduct = 1;
        int leftMax = Integer.MIN_VALUE;
        for (int i = mid; i >= left; i--) {
            leftProduct *= nums[i];
            leftMax = Math.max(leftMax, leftProduct);
        }
        
        int rightProduct = 1;
        int rightMax = Integer.MIN_VALUE;
        for (int i = mid + 1; i <= right; i++) {
            rightProduct *= nums[i];
            rightMax = Math.max(rightMax, rightProduct);
        }
        
        return Math.max(leftMax, leftMax * rightMax);
    }
}
```

# Memoized Approach
```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        Integer[][] memo = new Integer[nums.length][nums.length];
        return maxProductHelper(nums, 0, nums.length - 1, memo);
    }
    
    private int maxProductHelper(int[] nums, int left, int right, Integer[][] memo) {
        if (left == right) {
            return nums[left];
        }
        
        if (memo[left][right] != null) {
            return memo[left][right];
        }
        
        int mid = left + (right - left) / 2;
        int leftMax = maxProductHelper(nums, left, mid, memo);
        int rightMax = maxProductHelper(nums, mid + 1, right, memo);
        int crossMax = maxCrossProduct(nums, left, mid, right);
        
        memo[left][right] = Math.max(Math.max(leftMax, rightMax), crossMax);
        return memo[left][right];
    }
    
    private int maxCrossProduct(int[] nums, int left, int mid, int right) {
        int leftProduct = 1;
        int leftMax = Integer.MIN_VALUE;
        for (int i = mid; i >= left; i--) {
            leftProduct *= nums[i];
            leftMax = Math.max(leftMax, leftProduct);
        }
        
        int rightProduct = 1;
        int rightMax = Integer.MIN_VALUE;
        for (int i = mid + 1; i <= right; i++) {
            rightProduct *= nums[i];
            rightMax = Math.max(rightMax, rightProduct);
        }
        
        return Math.max(leftMax, leftMax * rightMax);
    }
}
```

# DP Approach
```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int maxProduct = nums[0];
        int minProduct = nums[0];
        int result = nums[0];

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(nums[i], maxProduct * nums[i]);
            minProduct = Math.min(nums[i], minProduct * nums[i]);

            result = Math.max(result, maxProduct);
        }

        return result;
    }
}
```

