[LRU Cache](https://leetcode.com/problems/lru-cache/)

# Intuition
The problem is to implement an LRU (Least Recently Used) cache data structure. The LRU cache works by evicting the least recently used key-value pair when the cache reaches its capacity, and it should provide constant time complexity for the `get` and `put` operations. The intuition is to use a combination of a hash map (or dictionary) and a doubly-linked list to efficiently track the key-value pairs and their access order.

# Approach
1. Use a hash map `map` to store the key-value pairs for constant time access.
2. Use a doubly-linked list `list` to store the keys in the order of their access. The most recently accessed key will be at the head of the list, and the least recently accessed key will be at the tail.
3. In the `get` operation:
   a. If the key is not present in the `map`, return -1.
   b. Otherwise, remove the key from its current position in the `list`, and move it to the head of the list.
   c. Return the value associated with the key.
4. In the `put` operation:
   a. If the key is already present in the `map`, update its value in the `map`, remove it from its current position in the `list`, and move it to the head of the list.
   b. If the key is not present in the `map`:
      - If the cache has reached its capacity, remove the least recently used key-value pair by removing the tail of the `list` and removing the corresponding entry from the `map`.
      - Insert the new key-value pair into the `map`, and add the new key to the head of the `list`.

# Complexity
- Time complexity:
  - `get`: O(1)
  - `put`: O(1)
* Space complexity: O(capacity)
The time complexity for both `get` and `put` operations is O(1) since the operations on the hash map and doubly-linked list take constant time on average. The space complexity is O(capacity) because the data structure will hold at most `capacity` key-value pairs.

# Code
```java
class LRUCache {
    int capacity;
    HashMap<Integer,Integer> map;
    LinkedList<Integer> list;
    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        list = new LinkedList<>();
    }
    
    public int get(int key) {
        if(!map.containsKey(key)) return -1;
        list.remove((Integer)key);
        list.addFirst(key);
        return map.get(key);
    }
    
    public void put(int key, int value) {
        if(map.containsKey(key)){
            map.put(key, value);
            list.remove((Integer)key);
            list.addFirst(key);
        }else{
            if(map.size()>=capacity){
                //evict key from the end
                int lruKey = list.removeLast();
                map.remove(lruKey);
            }
            map.put(key, value);
            list.addFirst(key);
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```