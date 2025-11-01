# Problem 150 - Evaluate Reverse Polish Notation

## Solution
- Did not watch NeetCode video before this problem
- This problem is meant for stacks. One good way that you can check if a problem is good for stacks is if it's kinda like tetris where
you add elements to a list of somesort and then eventually remove a few of the top once once some conditions evaluates to true. In this
problem, you will keep adding the integers to a list, until you reach an operator where you will then apply that operator on the last two added elements and then the result of that operation, you will then append back onto the list. Keep repeating until all operators are used up and then there will be one element left in the list which is your final answer.

### First Attempt
```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        operators = {
            "+": operator.add, 
            "-": operator.sub, 
            "*": operator.mul, 
            "/": lambda a, b: int(a / b)
        }
        for token in tokens:
            if token not in operators:
                stack.append(token)
            else:
                num2 = int(stack.pop())
                num1 = int(stack.pop())
                stack.append(operators[token](num1, num2))

        return int(stack[0])
```
SOLVED
- Time Complexity: O(n)
    - Need to iterate through all elements of the input string
- Space Compleity: O(n)
    - Creates a stack that increases in size as the input string increases in size