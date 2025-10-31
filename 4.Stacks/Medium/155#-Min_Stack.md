# Problem 155 - Min Stack

* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.
## Solution
- Popping, inserting, and getting the element at the top fo the stack are already O(1) time complexity so that part isn't tricky. The tricky
part is getting the minimum element. One way I will try to do this is that instead of inserting just integers into the stack, I will insert
a tuple formatted as (integer, minimum_element). By doing this, at each element of the stack, it will contain the minimum element at that point meaning the top most element will contain the minimum element of the whole stack.

### First Attempt
```
class MinStack:

    def __init__(self):
        self.stack = []

    def push(self, val: int) -> None:
        min_element = val if not self.stack else min(val, self.stack[-1][1])
        self.stack.append((val, min_element))

    def pop(self) -> None:
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1][0]

    def getMin(self) -> int:
        return self.stack[-1][1]


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
SOLVED:
- Time Complexity: O(1)
- Space Complexity: O(2n) -> O(n)