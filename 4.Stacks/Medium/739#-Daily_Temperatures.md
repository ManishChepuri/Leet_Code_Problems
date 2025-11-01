# Problem 739 - Daily Temperatures

## Solution
- DID NOT use NeetCode video solution for this
- This is another problem that can be easily solved with stacks. The trick is that the elements you add to the stack should be a tuple of the temperature and the index of the day of that temperature. Whenever you add an element to the stack, you just need to check if the temperature is greater than the previous temperature, and if so, then subtract the indicies of the temeratures and put that result into the the result list at the index of the subtracted temperature day.

### First Attempt
```
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = [] # pair: (temp, index)
        res = [0] * len(temperatures)

        for idx, temp in enumerate(temperatures):
            while stack and temp > stack[-1][0]:
                t, i = stack.pop()
                res[i] = idx - i
            stack.append((temp, idx))

        return res
```
SOLVED
- Time Complexity: O(n)
    - Must iterate through each element of input array
- Space Complexity: O(n)
    - Creates a stack and a result array that grows with as the input array grows