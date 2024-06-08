[Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/description/)

Deque
If we can add and remove elements from both sides of the sliding window, we can solve this problem in linear time. It turns out that we can use Deque to achieve the goal. In the Deque, we add and remove indices.

Basically, for each element nums[i] in the array that we are about to insert, we first check whether the leftmost index in the sliding window is out of bound. If so, we remove it by pollFirst() in constant time.

Then we continuously remove the rightmost indices if their corresponding elements are less than nums[i] (the element we are about to insert). The idea is that the elements that are less than the element we'll insert won't have any contributions to the maximum element of the sliding window. So it is safe to remove them.

After removal pollLast() and insertion offerLast(i) (the element nums[i]), we can say that the leftmost element in the window is maximum. Think about it why. Notice that the maximum element could be the one we just insert.

Last but not least, adding the maximum elements to the result array when necessary.

# Intuition
The problem is to find the maximum value in each sliding window of size `k` in an array `nums`. The intuition is to use a deque (double-ended queue) to store the indices of the elements in the current window. By maintaining the deque in a way that the front element is always the maximum value in the current window, we can efficiently find the maximum value for each window.

# Approach
1. Initialize an empty deque `win` to store the indices of elements in the current window.
2. Iterate through the array `nums` using a pointer `i`.
3. For each element `nums[i]`:
   a. Remove the indices from the front of the deque that are out of the current window's bounds (i.e., `win.peekFirst() <= i - k`).
   b. Remove the indices from the end of the deque whose corresponding values are less than `nums[i]`, as they will never be the maximum value in any future window.
   c. Add the current index `i` to the end of the deque.
   d. If `i >= k - 1` (the window has been filled), add the value at the front of the deque (`nums[win.peekFirst()]`) to the result array, as it is the maximum value in the current window.
4. Return the result array containing the maximum values for each sliding window.

# Complexity
- Time complexity: O(n)
* Space complexity: O(k)
The time complexity is O(n) because we iterate through the array once. The space complexity is O(k) because the deque can store at most `k` elements.

# Code
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // assume nums is not null
        int n = nums.length;
        if (n == 0 || k == 0) {
            return new int[0];
        }
        int[] result = new int[n - k + 1]; // number of windows
        Deque<Integer> win = new ArrayDeque<>(); // stores indices
        
        for (int i = 0; i < n; ++i) {
            // remove indices that are out of bound
            while (win.size() > 0 && win.peekFirst() <= i - k) {
                win.pollFirst();
            }
            // remove indices whose corresponding values are less than nums[i]
            while (win.size() > 0 && nums[win.peekLast()] < nums[i]) {
                win.pollLast();
            }
            // add nums[i]
            win.offerLast(i);
            // add to result
            if (i >= k - 1) {
                result[i - k + 1] = nums[win.peekFirst()];
            }
        }
        return result;
    }
}
```