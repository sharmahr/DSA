[Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/)

# Intuition
The problem is to find the number of days you have to wait after each day to get a warmer temperature. The intuition is to use a stack to keep track of the indices of the temperatures that are waiting for a warmer temperature. We can iterate through the temperatures in reverse order and update the answer for the indices in the stack whenever we encounter a warmer temperature.

# Approach
1. Create an array `answer` of the same length as `temperatures`, initialized with 0.
2. Create an empty stack `stack` to store the indices of the temperatures that are waiting for a warmer temperature.
3. Iterate through the `temperatures` array in reverse order:
   a. While the stack is not empty, and the current temperature is greater than or equal to the temperature at the top of the stack, pop the index from the stack and update the corresponding element in `answer` with the difference between the current index and the popped index.
   b. Push the current index onto the stack.
4. Return the `answer` array.

# Complexity
- Time complexity: O(n)
* Space complexity: O(n)
The time complexity is O(n) because we iterate through the `temperatures` array once, and the operations on the stack take constant time on average. The space complexity is O(n) in the worst case, when all temperatures are in decreasing order, and we need to store all indices in the stack.

# Code
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] answer = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && temperatures[i] >= temperatures[stack.peek()]) {
                stack.pop();
            }
            answer[i] = stack.isEmpty() ? 0 : stack.peek() - i;
            stack.push(i);
        }

        return answer;
    }
}
```