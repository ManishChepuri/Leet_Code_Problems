# Problem 424 - Longest Repeating Character Replacement

## Initial Thoughts
- Brute force method would be to first iterate thorugh every character of the string. Then for each character iterate from that character to the end of the string. Each top level iteration should define a count dictionary and a max substring variable. As you iterate through, add 1 to the index of each character and calculate the max between that and the maxf.

* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.

## Solution
- Use sliding window technique. Start with left pointer and right pointer at 0. Then slide right pointer to the right, updating count dictionary, as long as the len(window) - count of the most frequent element in the window is <= k. Keep repeating until the equation evaluates to false. Note the sized of the window and then keep incrementing the left pointer and removing elements from the count dictionary until the equation evaluates to true. Then keep repeating process until the right pointer reaches the end of the string.

### First Attempt
```
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        char_count = {}
        l = 0

        longest = 0
        for r in range(len(s)):
            char_count[s[r]] = char_count.get(s[r], 0) + 1
            while r - l + 1 - max(char_count.values()) > k:
                char_count[s[l]] = char_count.get(s[l]) - 1
                l += 1
            longest = max(longest, sum(char_count.values()))
        
        return longest
```
SOLVED