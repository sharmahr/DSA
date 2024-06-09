

# Intuition
The problem requires storing key-value pairs with timestamps and retrieving the value for a given key and timestamp. The intuition is to use a hash map to store the key-value pairs, where each key maps to a list of values along with their corresponding timestamps. To retrieve the value for a given key and timestamp, we can perform a binary search on the list of values to find the value with the highest timestamp less than or equal to the given timestamp.

# Approach
1. Create a nested class `Value` to store the value and its corresponding timestamp.
2. Initialize a hash map `store` to store the key-value pairs, where each key maps to a list of `Value` objects.
3. Implement the `set` method:
   - Get the list of values for the given key from the `store` map using `computeIfAbsent`. If the key doesn't exist, create a new list.
   - Add a new `Value` object with the given value and timestamp to the list.
4. Implement the `get` method:
   - Get the list of values for the given key from the `store` map.
   - If the list is null, return an empty string as the key doesn't exist.
   - Perform a binary search on the list of values to find the value with the highest timestamp less than or equal to the given timestamp.
   - If a valid value is found, return its corresponding value; otherwise, return an empty string.

# Complexity
- Time complexity: $O(\log n)$ for the `get` operation, where $n$ is the number of values for a given key. The `set` operation takes $O(1)$ time.
- Space complexity: $O(n)$, where $n$ is the total number of key-value pairs stored.

# Code
```java
class TimeMap {
    private static class Value {
        String value;
        int timestamp;

        Value(String value, int timestamp) {
            this.value = value;
            this.timestamp = timestamp;
        }
    }
    
    private Map<String, List<Value>> store;

    public TimeMap() {
        store = new HashMap<>();
    }

    public void set(String key, String value, int timestamp) {
        List<Value> values = store.computeIfAbsent(key, k -> new ArrayList<>());
        values.add(new Value(value, timestamp));
    }

    public String get(String key, int timestamp) {
        List<Value> values = store.get(key);
        if (values == null) {
            return "";
        }

        int left = 0;
        int right = values.size() - 1;
        int index = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            Value value = values.get(mid);
            if (value.timestamp <= timestamp) {
                index = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return index != -1 ? values.get(index).value : "";
    }
}
```