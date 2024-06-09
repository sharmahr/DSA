[Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/description/)

# Intuition
The problem can be solved using a binary search approach. The idea is to find the minimum possible eating speed that allows Koko to eat all the bananas within the given hour constraint. We can start with a minimum possible speed of 1 banana per hour and a maximum possible speed equal to the maximum pile size. Then, we can perform a binary search on the range of possible speeds and check if the current speed allows Koko to eat all the bananas within the given hour constraint.

# Approach
1. Initialize the left pointer (low) to 1, which is the minimum possible eating speed (1 banana per hour).
2. Initialize the right pointer (high) to the maximum pile size, which is the maximum possible eating speed.
3. Perform a binary search on the range [low, high]:
   a. Calculate the mid value between low and high.
   b. Use a helper function to calculate the number of hours needed to eat all the bananas at the current speed (mid).
   c. If the number of hours needed is greater than the given hour constraint (h), update low to mid + 1 (since the current speed is too slow).
   d. Otherwise, update high to mid (since the current speed might be the minimum possible speed).
4. After the binary search, the left pointer (low) will hold the minimum possible eating speed.

# Complexity
- Time complexity: O(n * log(max_pile_size)), where n is the number of piles. The binary search takes O(log(max_pile_size)) iterations, and in each iteration, we need to calculate the hours needed, which takes O(n) time.
- Space complexity: O(1), since we only use a constant amount of extra space.

# Code
```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int left = 1; // minimum possible speed
        int right = 0;
        for(int i:piles){
            right = Math.max(right, i);
        }
        while(left < right){
            int mid = left + (right-left)/2;
            int hoursNeeded = calculateHoursNeeded(piles, mid);
            if(hoursNeeded > h){
                left = mid + 1;
            }else{
                right = mid;
            }
        }
        return left;
    }

    private int calculateHoursNeeded(int[] piles, int k){
        int hours = 0;
        for(int i:piles){
            hours += Math.ceil((double)i/k);
        }
        return hours;
    }
}
```