[Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)

# Intuition
The problem is to evaluate a Reverse Polish Notation (RPN) expression. RPN is a notation where operators follow their operands. The intuition is to use a stack to evaluate the expression by pushing operands onto the stack and performing operations when an operator is encountered, using the operands from the top of the stack.

# Approach
1. Initialize an empty stack.
2. Iterate through each token in the input array:
   a. If the token is an operand (a number), push it onto the stack.
   b. If the token is an operator (+, -, *, /):
      - Pop the top two operands from the stack.
      - Perform the operation on the two operands.
      - Push the result back onto the stack.
3. After iterating through all tokens, the final result should be the only value left on the stack.

# Complexity
- Time complexity: O(n)
* Space complexity: O(n)
The time complexity is O(n), where n is the number of tokens in the input array, since we iterate through the array once. The space complexity is also O(n) in the worst case, when the input is a sequence of operands without any operators.

# Code
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<String> stack = new Stack<>();
        int result = 0;
        for(String s:tokens){
            if(s.equals("+") || s.equals("-") || s.equals("*") || s.equals("/")){
                int a = Integer.parseInt(stack.pop());
                int b = Integer.parseInt(stack.pop());
                
                if (s.equals("+")) stack.push(Integer.toString(a+b));
                else if (s.equals("-")) stack.push(Integer.toString(b-a));
                else if (s.equals("*")) stack.push(Integer.toString(a*b));
                else if (s.equals("/")) stack.push(Integer.toString(b/a));
            }else{
                stack.push(s);
            }
        }
        return Integer.parseInt(stack.pop());
    }
}
```