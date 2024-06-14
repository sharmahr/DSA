[Palindromic Partitioning](https://leetcode.com/problems/palindrome-partitioning/description/)

# Intuition
The problem of partitioning a string into palindromic substrings can be solved using a backtracking approach. The intuition is to generate all possible substrings of the given string and check if each substring is a palindrome. If a substring is a palindrome, it can be added to the current partition, and the process can be repeated for the remaining part of the string.

# Approach
1. Initialize an empty result list to store all the valid palindromic partitions.
2. Define a recursive function `backtrack` that takes the following parameters:
   - `s`: The input string.
   - `start`: The starting index of the current substring.
   - `current`: The current partition being built.
   - `result`: The list to store all the valid palindromic partitions.
3. In the `backtrack` function:
   - Base case: If the `start` index reaches the end of the string, add the current partition to the result list and return.
   - Iterate through the possible end indices of substrings starting from `start`:
     - Extract the substring from `start` to `end`.
     - Check if the substring is a palindrome using the `isPalindrome` helper function.
     - If the substring is a palindrome:
       - Add the substring to the current partition.
       - Recursively call `backtrack` with the updated `start` index (set to `end`) to generate partitions for the remaining part of the string.
       - Backtrack by removing the last added substring from the current partition.
4. Define a helper function `isPalindrome` that takes a string as input and checks if it is a palindrome.
5. Start the backtracking process by calling `backtrack` with the initial parameters.
6. Return the result list containing all the valid palindromic partitions.

# Complexity
- Time complexity: $O(2^n)$, where $n$ is the length of the string. In the worst case, when all substrings are palindromes, the algorithm generates all possible partitions, resulting in exponential time complexity.
- Space complexity: $O(n)$ for the recursive call stack. The maximum depth of recursion is equal to the length of the string.

# Code
```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(s, 0, new ArrayList<>(), result);
        return result;
    }

    void backtrack(String s, int start, List<String> current, List<List<String>> result){
        if(start == s.length()){
            result.add(new ArrayList<>(current));
            return;
        }

        for(int end=start+1; end <= s.length(); end++){
            String substring = s.substring(start, end);
            if(isPalindrome(substring)){
                current.add(substring);
                backtrack(s, end, current, result);
                current.remove(current.size() - 1);
            }
        }
    }

    private boolean isPalindrome(String s){
        int length = s.length()/2;
        for(int i=0;i<=length;i++){
            if(s.charAt(i) != s.charAt(s.length()-1-i)) return false;
        }
        return true;
    }
}
```