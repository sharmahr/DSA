[Top K frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

# Intuition
The problem requires finding the k most frequent elements in the given array. The intuitive approach is to use a hash map to count the frequency of each element and then use a priority queue (min-heap) to keep track of the top k frequent elements.

# Approach
1. Create a hash map to store the frequency of each element in the array.
2. Iterate through the array and update the frequency of each element in the hash map.
3. Create a priority queue (min-heap) to store the top k frequent elements.
4. Iterate through the entries of the hash map:
   - Create an Entry object with the element and its frequency.
   - Add the Entry object to the priority queue.
   - If the size of the priority queue exceeds k, remove the Entry with the lowest frequency.
5. Create an array of size k to store the result.
6. Iterate from k-1 to 0 and poll the top k elements from the priority queue and add them to the result array.
7. Return the result array.

# Complexity
- Time complexity: O(n log k), where n is the length of the input array and k is the number of top frequent elements to return. Adding each element to the heap takes O(log k) time, and we do this for all n elements in the worst case.
- Space complexity: O(n), where n is the length of the input array. In the worst case, the hash map will store all n elements, and the priority queue will store k elements.

# Code
```java
import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;

class Solution {

    class Entry implements Comparable<Entry> {
        int val;
        int frequency;
        Entry(int val, int frequency){
            this.val = val;
            this.frequency = frequency;
        }

        public int compareTo(Entry e){
            return Integer.compare(this.frequency, e.frequency);
        }
    }

    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Entry> heap = new PriorityQueue<>();
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int key = entry.getKey();
            int val = entry.getValue();
            heap.add(new Entry(key, val));
            if (heap.size() > k) {
                heap.poll();
            }
        }

        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = heap.poll().val;
        }
        return result;
    }
}
```