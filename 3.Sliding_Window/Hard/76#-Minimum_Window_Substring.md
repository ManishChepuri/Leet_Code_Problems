# Problem 76 - Minimum Window Substring

### Initial Thoughts
* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.

## Solution
Will implement sliding window technique as most problems with substrings need this technique. Need two dicts: one for the characters you need (the counts of chars in t) and one for the chars within the current sliding window. First initialize the need dict. Then need to declare variables to remember the min_substring length, l index of min_window and r index of min_window. The sliding window will be of variable size so start the r and l pointers on the first element. For each element you need to add it to the have dict if its in the need dict then increment the matches variable if the count within both dictionaries are exactly EQUAL. Then, you need to start incrementing the left pointer. While the matches are >= the desired amount, you have to decrement the count of the element at l from the have and then increment the left pointer. You need to keep track of the minimum size of the window while matches >= the desired amount. Once you finish iterating through the string s, you should have two pointers pointing to the left and right sides of the minimum window substring.

### First Attempt
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if len(t) > len(s):
            return ""

        need = {}
        for c in t:
            need[c] = need.get(c, 0) + 1

        matches = 0
        min_substring = float("infinity")
        min_r = -1
        min_l = -1
        have = {}
        l = 0
        for r, c in enumerate(s):
            if c in need:
                have[c] = have.get(c, 0) + 1
                if have[c] == need[c]:
                    matches += 1
            while matches >= len(need):
                if r - l + 1 < min_substring:
                    min_substring = r - l + 1
                    min_r = r
                    min_l = l
                if s[l] in need:
                    have[s[l]] -= 1
                    if have[s[l]] < need[s[l]]:
                        matches -= 1
                l += 1

        return s[min_l:min_r+1] if min_substring != float("infinity") else ""
```
SOLVED
