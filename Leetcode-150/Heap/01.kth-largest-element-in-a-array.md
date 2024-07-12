[Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

# Intuition
To find the kth largest element in an array, we can use a min-heap data structure. We can maintain a min-heap of size k, where the heap stores the k largest elements encountered so far. Whenever we encounter a new element, if it is larger than the smallest element in the min-heap (i.e., the root), we remove the root and insert the new element into the min-heap. This way, the root of the min-heap will always be the kth largest element.

# Approach
1. Create a min-heap `heap` using a `PriorityQueue` to store the k largest elements.
2. Iterate through the `nums` array:
   - If the size of the min-heap is greater than or equal to k:
     - If the current element `nums[i]` is greater than the root of the min-heap (i.e., `heap.peek()`):
       - Remove the root element from the min-heap using `heap.poll()`.
       - Add the current element `nums[i]` to the min-heap using `heap.add(nums[i])`.
   - If the size of the min-heap is less than k:
     - Add the current element `nums[i]` to the min-heap using `heap.add(nums[i])`.
3. After the loop ends, the root of the min-heap (obtained using `heap.peek()`) will be the kth largest element.
4. Return the root of the min-heap.

# Complexity
- Time complexity: $O(n \log k)$
Iterating through the `nums` array takes $O(n)$ time, where n is the number of elements in the array. For each element, we perform at most one removal and one insertion operation in the min-heap, each taking $O(\log k)$ time. Therefore, the overall time complexity is $O(n \log k)$.

* Space complexity: $O(k)$
The space complexity is determined by the size of the min-heap, which stores at most k elements. Therefore, the space complexity is $O(k)$.

# Code
```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> heap = new PriorityQueue<>();
        
        for (int i = 0; i < nums.length; i++) {
            if (heap.size() >= k) {
                if (heap.peek() < nums[i]) {
                    heap.poll();
                    heap.add(nums[i]);
                }
            } else {
                heap.add(nums[i]);
            }
        }
        
        return heap.peek();
    }
}
```