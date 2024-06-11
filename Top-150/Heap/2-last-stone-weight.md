[Last Stone Weight](https://leetcode.com/problems/last-stone-weight/description/) 

# Intuition
To solve the Last Stone Weight problem, we can use a max-heap data structure. We can add all the stones to the max-heap and then repeatedly remove the two heaviest stones, smash them together, and add the resulting stone (if any) back to the heap until there is at most one stone left. The weight of the remaining stone (if any) will be the result.

# Approach
1. Create a max-heap `heap` using a `PriorityQueue` with `Collections.reverseOrder()` as the comparator to store the stones in descending order.
2. Iterate through the `stones` array and add each stone to the max-heap using `heap.add(stones[i])`.
3. While the size of the max-heap is greater than 1, do the following:
   - Remove the two heaviest stones from the max-heap using `heap.poll()` and store them in variables `x` and `y`.
   - If `x` is not equal to `y`, calculate the difference `x - y` and add it back to the max-heap using `heap.add(x - y)`.
4. After the loop ends, if the size of the max-heap is equal to 1, return the remaining stone's weight using `heap.peek()`.
5. If the max-heap is empty, return 0 as there are no stones left.

# Complexity
- Time complexity: $O(n \log n)$
Adding all the stones to the max-heap takes $O(n \log n)$ time, where n is the number of stones. In the worst case, we need to perform the smashing operation for each pair of stones, which takes $O(\log n)$ time for each operation due to the heap operations (removal and insertion). Therefore, the overall time complexity is $O(n \log n)$.

* Space complexity: $O(n)$
The space complexity is determined by the size of the max-heap, which can store at most n stones. Therefore, the space complexity is $O(n)$.

# Code
```java
class Solution {
    public int lastStoneWeight(int[] stones) {
        PriorityQueue<Integer> heap = new PriorityQueue<>(Collections.reverseOrder()); // max heap
        
        for (int i = 0; i < stones.length; i++) {
            heap.add(stones[i]);
        }
        
        while (heap.size() > 1) {
            int x = heap.poll();
            int y = heap.poll();
            
            if (x != y) {
                heap.add(x - y);
            }
        }
        
        if (heap.size() == 1) {
            return heap.peek();
        }
        
        return 0;
    }
}
```