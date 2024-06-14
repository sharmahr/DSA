[Hand of Straights](https://leetcode.com/problems/hand-of-straights/description/)

# Intuition
To determine if a hand of cards can be arranged into groups of a specific size, we can use a greedy approach along with a hashmap to keep track of the frequency of each card. The intuition is to sort the hand and process the cards in ascending order. For each card, we check if we can form a group of the given size by checking the frequency of the consecutive cards in the hashmap. If any card is missing or has a frequency of zero, it means we cannot form a group, and the hand is not a valid arrangement.

# Approach
1. Check if the length of the hand is divisible by the group size. If not, return false since we cannot form groups of the given size.
2. Create a hashmap to store the frequency of each card in the hand.
3. Sort the hand in ascending order.
4. Iterate through each card in the sorted hand:
   - If the frequency of the current card is zero or less, skip it since it has already been processed.
   - For each consecutive card (from the current card to the current card + group size - 1):
     - Check the frequency of the consecutive card in the hashmap.
     - If the frequency is greater than zero, decrement the frequency by one.
     - If the frequency is zero, return false since we cannot form a group.
   - Decrement the frequency of the current card in the hashmap.
5. If we have processed all cards without returning false, return true since the hand can be arranged into groups of the given size.

# Complexity
- Time complexity: O(n log n), where n is the length of the hand. Sorting the hand takes O(n log n) time, and iterating through the sorted hand takes O(n) time.
- Space complexity: O(n) to store the frequency of each card in the hashmap.

# Code
```java
class Solution {
    public boolean isNStraightHand(int[] hand, int groupSize) {
        if(hand.length % groupSize != 0) return false;
        
        // store the number and the frequency of the elements
        Map<Integer, Integer> map = new HashMap<>();
        for(int i: hand){
            map.put(i, map.getOrDefault(i, 0) + 1);
        }
        Arrays.sort(hand);
        for(int card : hand){
            if(map.get(card) <= 0) continue;
            for(int i=0;i<groupSize;i++){
                int count = map.getOrDefault(card + i, 0); // find if the consecutive in hashmap
                if(count > 0){
                    map.put(card + i, count - 1);
                }else{
                    return false;
                }
            }
            map.put(card, map.get(card) - 1); // process the card
        }

        return true;
    }
}
```