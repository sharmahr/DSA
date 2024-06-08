[Min Stack](https://leetcode.com/problems/min-stack/)

# Intuition
The problem is to design a data structure that supports push, pop, top, and getMin operations in constant time. The intuition is to use a stack to store the elements and maintain a variable `min` to keep track of the minimum element at any given time. However, we need a way to remember the previous minimum value when a new minimum value is pushed onto the stack.

# Approach
1. Initialize a variable `min` to store the current minimum value, initially set to `Integer.MAX_VALUE`.
2. Initialize a stack `stack` to store the elements.
3. In the `push` operation:
   a. If the new element `x` is less than or equal to the current `min`, push the current `min` onto the stack (to remember the previous minimum), and update `min` to `x`.
   b. Push `x` onto the stack.
4. In the `pop` operation:
   a. If the top element of the stack is equal to the current `min`, pop twice from the stack. The second popped element is the new `min`.
   b. Otherwise, pop the top element from the stack.
5. In the `top` operation, return the top element of the stack.
6. In the `getMin` operation, return the current `min`.

# Complexity
- Time complexity:
  - `push`: O(1)
  - `pop`: O(1)
  - `top`: O(1)
  - `getMin`: O(1)
* Space complexity: O(n)
The space complexity is O(n) because we use an additional stack to store the elements.

# Code
```java
class MinStack {
    int min = Integer.MAX_VALUE;
    Stack<Integer> stack = new Stack<Integer>();
    public void push(int x) {
        // only push the old minimum value when the current 
        // minimum value changes after pushing the new value x
        if(x <= min){          
            stack.push(min);
            min=x;
        }
        stack.push(x);
    }

    public void pop() {
        // if pop operation could result in the changing of the current minimum value, 
        // pop twice and change the current minimum value to the last minimum value.
        if(stack.pop() == min) min=stack.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```