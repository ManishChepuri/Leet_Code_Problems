# Problem 1768 - Merge String Alternately

### Initial Thoughts
Just iterate through while i is less than the length of both strings and then alternate appending to the result string. At the end just add the string with
remaining letters to the end of the result string.


### Easy Solution First Try:
```
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        i = 0
        res = ""
        while i < len(word1) and i < len(word2):
            res += word1[i]
            res += word2[i]
            i += 1
        res += word1[i:] + word2[i:]
        return res
```
