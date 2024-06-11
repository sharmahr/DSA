[Kth Largest Element in a stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

# Intuition
To find the kth largest element in a stream of integers, we can use a min-heap data structure. The min-heap will store the k largest elements encountered so far. Whenever a new element is added, if it is larger than the smallest element in the min-heap (i.e., the root), we remove the root and insert the new element into the min-heap. This way, the root of the min-heap will always be the kth largest element.

# Approach
1. Initialize an integer variable `k` to store the value of k (the position of the largest element we want to find).
2. Initialize a min-heap `heap` to store the k largest elements.
3. In the constructor `KthLargest(int k, int[] nums)`:
   - Assign the value of k to the `k` variable.
   - Create a new `PriorityQueue` (min-heap) and assign it to the `heap` variable.
   - Iterate through the `nums` array and add each element to the min-heap by calling the `add` method.
4. In the `add(int val)` method:
   - If the size of the min-heap is greater than or equal to k:
     - If the new element `val` is greater than the root of the min-heap (i.e., `heap.peek()`):
       - Remove the root element from the min-heap using `heap.poll()`.
       - Add the new element `val` to the min-heap using `heap.add(val)`.
   - If the size of the min-heap is less than k:
     - Add the new element `val` to the min-heap using `heap.add(val)`.
   - Return the root element of the min-heap, which represents the kth largest element.

# Complexity
- Time complexity: $O(\log k)$ for each `add` operation, $O(n \log k)$ for the constructor
In the constructor, we iterate through the `nums` array of size n and add each element to the min-heap. Each `add` operation takes $O(\log k)$ time since the min-heap has at most k elements. Therefore, the time complexity of the constructor is $O(n \log k)$.
For each `add` operation, we perform at most one removal and one insertion in the min-heap, both of which take $O(\log k)$ time. Therefore, the time complexity of each `add` operation is $O(\log k)$.

* Space complexity: $O(k)$
The space complexity is determined by the size of the min-heap, which stores at most k elements. Therefore, the space complexity is $O(k)$.

# Code
```java
class KthLargest {
    int k;
    PriorityQueue<Integer> heap;
    
    public KthLargest(int k, int[] nums) {
        this.k = k;
        this.heap = new PriorityQueue<>(); // min heap

        // Add the elements in the heap
        for (int i = 0; i < nums.length; i++) {
            add(nums[i]);
        }
    }
    
    public int add(int val) {
        if (heap.size() >= k) {
            if (heap.peek() < val) {
                // Remove the smallest element and add the new element
                heap.poll();
                heap.add(val);
            }
        } else {
            heap.add(val);
        }
        return heap.peek();
    }
}
```