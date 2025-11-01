# Problem 20 - Valid Parenthesis

## Solution
- This problem is meant for stacks. As you iterate through the input string, if the element is an open parenthesis then append it to
the stack. If its a close, then if the top element of the stack doesn't match the type of the close parenthesis then just you return False, otherwise remove the top element of the stack and don't add the close parenthesis. At the end of the iteration, if the stack is empty then the string was valid, otherwise the string was invalid

### First Attempt:
```
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        close_to_open = {")" : "(", "]" : "[", "}" : "{"}
        for r, c in enumerate(s):
            if c in close_to_open:
                if stack and stack[-1] == close_to_open[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)

        return False if stack else True
```
SOLVED
- TimeComplexity = O(n)
    - You are iterating through the input string
- Space Complexity = O(n)
    - Size of the stack is growing with the size of the input string