[K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/description/)

# Intuition
To find the k closest points to the origin, we can calculate the distance of each point from the origin and use a max-heap to store the k closest points. The max-heap will store the points based on their distances from the origin in descending order. If a point has a smaller distance than the top element of the max-heap, we remove the top element and add the new point to the heap. This way, the max-heap will always maintain the k closest points.

# Approach
1. Create a custom class `Element` that implements the `Comparable` interface to represent a point. The `Element` class has properties `x`, `y`, and `distance` to store the x-coordinate, y-coordinate, and the squared distance from the origin, respectively.
2. Implement the `compareTo` method in the `Element` class to compare elements based on their distances in descending order.
3. Create a max-heap `heap` using a `PriorityQueue` to store the `Element` objects.
4. Iterate through the `points` array:
   - Create an `Element` object `temp` for each point using its x and y coordinates.
   - If the size of the max-heap is greater than or equal to k:
     - If the distance of `temp` is smaller than the distance of the top element of the max-heap (obtained using `heap.peek().distance`):
       - Remove the top element from the max-heap using `heap.poll()`.
       - Add `temp` to the max-heap using `heap.add(temp)`.
   - If the size of the max-heap is less than k:
     - Add `temp` to the max-heap using `heap.add(temp)`.
5. Create a 2D array `result` of size `k` to store the k closest points.
6. Iterate k times:
   - Remove the top element from the max-heap using `heap.poll()` and store it in `temp`.
   - Store the x and y coordinates of `temp` in `result[i][0]` and `result[i][1]`, respectively.
7. Return the `result` array containing the k closest points.

# Complexity
- Time complexity: $O(n \log k)$
Iterating through the `points` array takes $O(n)$ time, where n is the number of points. For each point, we perform at most one removal and one insertion operation in the max-heap, each taking $O(\log k)$ time. Therefore, the overall time complexity is $O(n \log k)$.

* Space complexity: $O(k)$
The space complexity is determined by the size of the max-heap, which stores at most k elements, and the `result` array, which also has a size of k. Therefore, the space complexity is $O(k)$.

# Code
```java
class Solution {
    class Element implements Comparable<Element> {
        long distance;
        int x, y;
        
        Element(int x, int y) {
            this.x = x;
            this.y = y;
            this.distance = (long) x * x + (long) y * y;
        }

        public int compareTo(Element e) {
            return Long.compare(e.distance, this.distance);
        }
    }
    
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<Element> heap = new PriorityQueue<>();
        
        for (int i = 0; i < points.length; i++) {
            Element temp = new Element(points[i][0], points[i][1]);
            if (heap.size() >= k) {
                if (temp.distance < heap.peek().distance) {
                    heap.poll(); // remove the top element
                    heap.add(temp);
                }
            } else {
                heap.add(temp);
            }
        }

        int[][] result = new int[k][2];
        for (int i = 0; i < k; i++) {
            Element temp = heap.poll();
            result[i][0] = temp.x;
            result[i][1] = temp.y;
        }
        return result;
    }
}
```