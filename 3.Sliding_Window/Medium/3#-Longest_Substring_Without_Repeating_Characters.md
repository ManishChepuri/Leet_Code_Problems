# Problem 3 - Longest Substring Without Repeating Characters

### Initial Thoughts
- Try to find the first letter of the substring. In a different problem that was using numbers we turned the input list into a set and then checked for each number in set if the num - 1 was in the set. If not, then that number was the start of a sequence. In this problem you could try to turn letters in ASCII values but the sequences in this problem are not based on alphabetical order.
- The Brute Force method would Time Complexity of O(n). It would be to iterate through each character and then check how far you could increment up the string before running into a duplicate. Then just return the length of the longest substring.

* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.

## Solution
- The Brute Force way has a lot of repitition. To avoid this we need to use the Sliding Window strategy. We first find the longest substring starting at the frist character. Then we increment the left and right side of the substring up 1. Then we see if we can increase the window. If we can then we increase the right side of the window by one. We repeat this until we can't increase the window. Then we shift the element by 1 again. If there is a duplicate added then we keep shifting until there isn't a duplicate. At the end we return the size of the window.

### First Attempt
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        unique_window = set()

        l, r = 0, 0
        pre_size = len(unique_window)
        unique_window.add(s[r])
        while r < len(s):
            # Keep increasing size if not adding duplicates
            while len(unique_window) > pre_size and r < len(s):
                r += 1
                pre_size = len(unique_window)
                unique_window.add(s[r])
            print(l, r)
            print(s[l], s[r])
            print()
            unique_window.remove(s[l])
            unique_window.add(s[r])
            r += 1
            l += 1
```

### Final Attempt
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        unique_window = set()
        l = 0

        max_len = 0
        for r in range(len(s)):
            while s[r] in unique_window:
                unique_window.remove(s[l])
                l += 1
            unique_window.add(s[r])
            max_len = max(max_len, len(unique_window))

        return max_len
```
SOLVED
