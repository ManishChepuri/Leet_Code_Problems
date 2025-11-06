# Problem 853 - Car Fleet

* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.

## Solution
- All you need to check is if two cars come into contact with each other, then count that as one car pretty much. So if you iterate backwards through a list of all the cars positions and speeds sorted in reverse, and start adding the cars to a stack, if the next car (which would be a car located in a lower position) somehow could get to the target in less time, then don't add that car to the stack. In the end you just return the length of the stack which is the number of car fleets

### Final Attempt
```
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        stack = []
        for p, s in sorted(list(zip(position, speed)), key=lambda x: x[0], reverse=True):
            time = (target - p) / s
            if not stack or time > stack[-1]: stack.append(time) 
        return len(stack)
```
SOLVED
- Time Complexity: O(nlogn)
- Space Complexity: O(n)