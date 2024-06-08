[Best time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

# Intuition
The problem is to find the maximum profit that can be made by buying and selling a stock once. The intuition behind the solution is to keep track of the minimum price seen so far and the maximum profit that can be made by selling at the current price. We can iterate through the prices and update the minimum price and maximum profit accordingly.

# Approach
1. Initialize the minimum price seen so far (`min`) to the first price in the array.
2. Initialize the maximum profit (`maxProfit`) to 0.
3. Iterate through the prices array starting from the second element.
4. For each price, check if it is less than the current minimum price. If so, update the minimum price.
5. Calculate the potential profit by subtracting the minimum price from the current price.
6. Update the maximum profit if the potential profit is greater than the current maximum profit.
7. Return the maximum profit after iterating through all prices.

# Complexity
- Time complexity: O(n)
* Space complexity: O(1)

# Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int length = prices.length;
        int min = prices[0];
        int maxProfit = 0;
        for (int i = 1; i < length; i++) {
            if (prices[i] < min) {
                min = prices[i];
            }
            maxProfit = Math.max(maxProfit, prices[i] - min);
        }
        return maxProfit;
    }
}
```