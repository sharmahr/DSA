[Encode and Decode Strings](https://neetcode.io/problems/string-encode-and-decode)

# Intuition
The problem requires encoding a list of strings into a single string and then decoding the encoded string back into the original list of strings. The intuitive approach is to use a delimiter to separate the individual strings and include the length of each string before the delimiter to facilitate the decoding process.

# Approach
Encoding:
1. Create an empty StringBuilder to store the encoded string.
2. Iterate through each string in the input list:
   - Append the length of the current string to the StringBuilder.
   - Append a delimiter (e.g., '#') to the StringBuilder.
   - Append the current string itself to the StringBuilder.
3. Return the resulting encoded string.

Decoding:
1. Create an empty list to store the decoded strings.
2. Initialize a pointer i to 0, which represents the current position in the encoded string.
3. While i is less than the length of the encoded string:
   - Initialize a pointer j to i.
   - Move j forward until it reaches the delimiter '#'.
   - Extract the length of the current string by taking the substring from i to j and convert it to an integer.
   - Move i to the position after the delimiter and the length of the current string.
   - Extract the current string by taking the substring from j+1 to i and add it to the list.
4. Return the list of decoded strings.

# Complexity
- Time complexity: O(n), where n is the total length of all the strings in the input list. The encoding process iterates through each character of each string once, and the decoding process iterates through each character of the encoded string once.
- Space complexity: O(n), where n is the total length of all the strings in the input list. The encoded string and the decoded list of strings both require space proportional to the total length of the strings.

# Code
```java
class Solution {

    public String encode(List<String> strs) {
        StringBuilder encodedString = new StringBuilder();
        for (String str : strs) {
            encodedString.append(str.length()).append("#").append(str);
        }
        return encodedString.toString();
    }

    public List<String> decode(String str) {
        List<String> list = new ArrayList<>();
        int i = 0;
        while (i < str.length()) {
            int j = i;
            while (str.charAt(j) != '#') j++;

            int length = Integer.valueOf(str.substring(i, j));
            i = j + 1 + length;
            list.add(str.substring(j + 1, i));
        }
        return list;
    }
}
```