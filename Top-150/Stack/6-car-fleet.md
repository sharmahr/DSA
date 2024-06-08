[Car Fleet](https://leetcode.com/problems/car-fleet/description/)

# Intuition
The problem is to determine the number of car fleets that will arrive at the destination, given the positions and speeds of the cars. The key observation is that if a car catches up to another car or fleet, it will slow down to match their speed. This means that cars or fleets with the same time to reach the destination will form a single fleet. We can calculate the time it takes for each car to reach the destination and sort them in descending order. Then, we can iterate through the sorted times and group cars with the same time into a fleet.

# Approach
1. Create a list `times` to store the time it takes for each car to reach the destination, calculated as `(target - position[i]) / speed[i]`.
2. Sort the `times` list in descending order.
3. Initialize a variable `fleets` to keep track of the number of car fleets.
4. Initialize a variable `prev_time` to store the time of the previous car or fleet.
5. Iterate through the sorted `times` list:
   a. If the current time is greater than `prev_time`, it means this car cannot catch up to the previous fleet, so it forms a new fleet. Increment `fleets` and update `prev_time` with the current time.
   b. If the current time is less than or equal to `prev_time`, it means this car will catch up to the previous fleet and slow down to match their speed.
6. Return `fleets` as the number of car fleets that will arrive at the destination.

# Complexity
- Time complexity: O(n log n)
* Space complexity: O(n)
The time complexity is O(n log n) due to the sorting operation. The space complexity is O(n) since we create a list of size `n` to store the times.

# Code
```java
class Solution {
    public int carFleet(int target, int[] position, int[] speed) {
        int n = position.length;
        double[] times = new double[n];
        
        // Calculate the time it takes for each car to reach the destination
        for (int i = 0; i < n; i++) {
            times[i] = (double) (target - position[i]) / speed[i];
        }
        
        // Sort the times in descending order
        Arrays.sort(times);
        
        int fleets = 0;
        double prev_time = Double.MIN_VALUE;
        
        for (double time : times) {
            if (time > prev_time) {
                fleets++;
                prev_time = time;
            }
        }
        
        return fleets;
    }
}
```