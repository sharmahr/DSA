[Meeting Rooms 2](https://neetcode.io/problems/meeting-schedule-ii)

# Intuition
To find the minimum number of meeting rooms required, we can use a min-heap to keep track of the end times of ongoing meetings. The intuition is to sort the intervals by start time and then iterate through them. For each interval, if the earliest meeting in the min-heap has ended before the current meeting starts, we can reuse that room. Otherwise, we need to allocate a new room. The size of the min-heap at the end represents the minimum number of rooms required.

# Approach
1. If the intervals list is null or empty, return 0 since no rooms are required.
2. Sort the intervals by start time in ascending order.
3. Create a min-heap to store the end times of ongoing meetings.
4. Iterate through each interval:
   - If the min-heap is not empty and the earliest meeting in the min-heap has ended before the current meeting starts (i.e., the peek of the min-heap is less than or equal to the start time of the current interval), remove that meeting from the min-heap.
   - Add the end time of the current meeting to the min-heap.
5. The size of the min-heap at the end represents the minimum number of rooms required.

# Complexity
- Time complexity: O(n log n), where n is the number of intervals. Sorting the intervals takes O(n log n) time, and iterating through the intervals takes O(n) time. Each operation on the min-heap (offer and poll) takes O(log n) time.
- Space complexity: O(n) to store the min-heap, which can contain at most n elements.

# Code
```java
/**
 * Definition of Interval:
 * public class Interval {
 *     public int start, end;
 *     public Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

class Solution {
    public int minMeetingRooms(List<Interval> intervals) {
        if (intervals == null || intervals.size() == 0) return 0;

        // Sort intervals by start time
        intervals.sort((a, b) -> a.start - b.start);

        // Min-heap to track end times of meetings
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (Interval interval : intervals) {
            // If the room due to free up the earliest is free, remove it from the heap
            if (!minHeap.isEmpty() && minHeap.peek() <= interval.start) {
                minHeap.poll();
            }
            // Add the current meeting's end time to the heap
            minHeap.offer(interval.end);
        }

        // The size of the heap is the number of rooms required
        return minHeap.size();
    }
}
```