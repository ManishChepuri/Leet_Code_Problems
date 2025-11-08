# Problem 735 - Asteroid Collision

## Solution
- For this one you need to use a stack and just check every possible scenario that could happen. First, there are some initial rules. An asteroid collision can only happen if the top of the stack is positive and the current asteroid is negative. If this condition were to come true, if the current asteroid is bigger than the top of the stack, we keep removing asteroids from the top of the stack until we can't anymore. If the current asteroid is smaller than the top of the stack, then we don't add the current asteroid to the top of the stack. If the current asteroid is the same size as the top of the stack, then we remove the asteroid from the top of the stack and don't add the current asteroid. If incoming asteroid is postive or its negative and the asteroid at the top of the stack is also negative, then we just add the current asteroid to the top of the stack

### First Attempt
```
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []

        for a in asteroids:
            if a < 0:
                while stack and stack[-1] > 0 and abs(a) > stack[-1]: 
                    stack.pop()
                if not stack or stack[-1] < 0: 
                    stack.append(a)
                elif abs(a) == stack[-1]: 
                    stack.pop()
            else: 
                stack.append(a)

        return stack
```
SOLVED
- Time Complexity: O(n)
    - Must iterate through every element of the input array
- Space Complexity: O(n)
    - Must create an output stack that grows in size as the input array gets larger