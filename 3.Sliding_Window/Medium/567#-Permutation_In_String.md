# Problem 567 - Permutation in String

### Initial Thoughts
- One easy way to do it is just to check if each letter of s1 is in s2 but that would result in time complexity of O(m*n)
- The recommended Space Complexity is O(1) meaning you can't create new data structures of size n.
- You can try to implement a sliding window of size len(s1). The sliding window won't increase or decrease in size as it iterates through.

* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.
## Solution
- Utilize sliding window technique. First make two arrays (for s1 and s2) of size 26 initialized to 0. Then iterate through both strings len(s1) times and increment the index of the ASCII value in each strings corresponding list. Now you have initialized the counts of characters in s1 and the counts of the characters in the first window of s2. This was done in O(len(s1)) TC and O(26) SC. Now you want to find the matches. To do this, you just need to iterate through the length of the lists and check if the counts at those indicies are the same. If so add 2 to matches and if not add 0. This was your first window so if the matches == 26 already, then return True. Now we will start the sliding window technique. Start r on the next letter past the window. If the current count of that character in the two lists already equal then you must decrement the matches variable by 1 as you are about to change the count. Then change the count in the s2 list. If the counts between the two lists now match then increment matches, but if not then don't change matches. Now you do the same for l, but you will decrement the count of the index of that character for s2. After you do your checks, you will then increment the left side of the sliding window. Then return True if the matches == 26, else continue.

### First Attempt
```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        if len(s1) > len(s2): return False
        
        s1_count = [0] * 26
        s2_count = [0] * 26

        for i in range(len(s1)):
            s1_count[ord(s1[i]) - ord('a')] += 1
            s2_count[ord(s2[i]) - ord('a')] += 1

        matches = 0
        for i in range(26):
            matches += (1 if s1_count[i] == s2_count[i] else 0)

        if matches == 26: return True

        l = 0
        for r in range(len(s1), len(s2)):

            r = ord(s2[r]) - ord('a')
            print(r)
            # Increment r
            if s2_count[r] == s1_count[r]:
                matches -= 1
            s2_count[r] += 1
            matches += (1 if s2_count[r] == s1_count[r] else 0)
            

            l_idx = ord(s2[l]) - ord('a')
            # Decrement l
            if s2_count[l_idx] == s1_count[l_idx]:
                matches -= 1
            s2_count[l_idx] -= 1
            matches += (1 if s2_count[l_idx] == s1_count[l_idx] else 0)
            l += 1

            # Return True if matches is 26
            if matches == 26: return True
        
        return False
```
SOLVED
TC = O(n); SC = O(26)
