[Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/description/)

# Intuition
To find the median from a data stream, we can use a two-heap approach. By maintaining a max-heap for the lower half of the numbers and a min-heap for the upper half of the numbers, we can efficiently access the middle element(s) to calculate the median. The key intuition is to balance the heaps so that the size difference between them is at most 1, and the top element of the max-heap is smaller than or equal to the top element of the min-heap.

# Approach
1. Initialize two heaps: `maxHeap` (max-heap) for the lower half of the numbers and `minHeap` (min-heap) for the upper half of the numbers.
2. When `addNum` is called:
   - Add the new number to `maxHeap`.
   - If `maxHeap` is not empty, `minHeap` is not empty, and the top element of `maxHeap` is greater than the top element of `minHeap`, remove the top element from `maxHeap` and add it to `minHeap`.
   - Balance the heaps by ensuring the size difference between them is at most 1. If `maxHeap` has more elements than `minHeap` by more than 1, remove the top element from `maxHeap` and add it to `minHeap`. Similarly, if `minHeap` has more elements than `maxHeap` by more than 1, remove the top element from `minHeap` and add it to `maxHeap`.
3. When `findMedian` is called:
   - If both heaps have the same size, return the average of the top elements of both heaps.
   - If `maxHeap` has more elements, return the top element of `maxHeap`.
   - If `minHeap` has more elements, return the top element of `minHeap`.

# Complexity
- Time complexity:
  - `addNum`: O(log n), where n is the number of elements in the data stream. Adding an element to a heap takes logarithmic time.
  - `findMedian`: O(1), as we can access the top elements of the heaps in constant time.

* Space complexity: O(n)
  - The space complexity is O(n), where n is the number of elements in the data stream. We store all the elements in the heaps.

# Code
```java
class MedianFinder {
    private PriorityQueue<Integer> maxHeap; // lower half of numbers
    private PriorityQueue<Integer> minHeap; // upper half of numbers

    public MedianFinder() {
        maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        minHeap = new PriorityQueue<>();
    }

    public void addNum(int num) {
        // Add the new number to the max-heap
        maxHeap.offer(num);

        // Balance the heaps if necessary
        if (!maxHeap.isEmpty() && !minHeap.isEmpty() && maxHeap.peek() > minHeap.peek()) {
            int maxNum = maxHeap.poll();
            minHeap.offer(maxNum);
        }

        // Ensure the size difference between heaps is at most 1
        if (maxHeap.size() > minHeap.size() + 1) {
            int maxNum = maxHeap.poll();
            minHeap.offer(maxNum);
        } else if (minHeap.size() > maxHeap.size() + 1) {
            int minNum = minHeap.poll();
            maxHeap.offer(minNum);
        }
    }

    public double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else if (maxHeap.size() > minHeap.size()) {
            return maxHeap.peek();
        } else {
            return minHeap.peek();
        }
    }
}
```