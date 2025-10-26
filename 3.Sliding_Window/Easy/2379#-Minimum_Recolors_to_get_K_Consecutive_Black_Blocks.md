# Problem 2379 - Minimum Recolors to Get K Consecutive Black Blocks

### Initial Thoughts
- Use sliding window technique. As you iterate through the string you need to keep track of two variables: minimum operations and number of black boxes. First you need to initialize the first sliding window. To do this just start iterating through the string and incrementing the num_black variable by 1 each time you reach a "B". Keep iterating until you get to the k - 1 index. Then you should calculate the if k - the number of black blocks is less than the previous min. Then increment the left pointer of the sliding window by 1 and removing one from the count of the black blocks if it is a "B" that you are removing from the sliding window. Keep repeating until the right pointer gets to the end of the string

## Solution
### First Attempt
```
class Solution:
    def minimumRecolors(self, blocks: str, k: int) -> int:
        l = 0
        num_black = 0
        min_operations = k
        for r in range(len(blocks)):
            if blocks[r] == "B":
                num_black += 1
            if r < k - 1:
                continue
            min_operations = min(min_operations, k - num_black)
            if blocks[l] == "B":
                num_black -= 1
            l += 1
        
        return min_operations
```
SOLVED
Time Complexity: O(n)
Space Complexity: O(1)