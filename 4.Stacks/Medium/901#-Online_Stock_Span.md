# Problem 901 - Online Stock Span

## Solution
- The Brute Force method for this problem would be for each element, add it to an array and then check how many days before that element the current element is greater than or equal to and then return that value. This approach, however, would be O(n^2). It is possible to do it in O(n), however.
- To do it in O(n), you must take advantage of *monotonic decreasing stacks*. What you need to do is first initialize a stack. Then for each element, when you add it to the stack, you need to add a tuple of the element paired with how many elements before it were less than or equals to that price. Then you add that to the stack. By doing this, whenever you get a new element, if its greater than the element you just added then you know that its also greater than all the elements before that one that you just added. For example if you just added the element (75, 3) to the stack. If the next price is 80, then you know that when you add 80 to the stack, the 1st index of the tuple will be gauranteed to be at least 3 since 80 > 75. So then you pop 75 from the stack and then keep checking if 80 is greater than previous elements.

### Answer
```
class StockSpanner:

    def __init__(self):
        self.stack = []

    def next(self, price: int) -> int:
        count = 0
        while self.stack and price >= self.stack[-1][0]:
            count += 1 + self.stack[-1][1]
            self.stack.pop()
        self.stack.append((price, count))
        return count + 1


# Your StockSpanner object will be instantiated and called as such:
# obj = StockSpanner()
# param_1 = obj.next(price)
```
SOLVED
- Time Complexity:
    - O(n) - Monotonic Decreasing Stack
- Space Complexity
    - O(n) - The stack created worst case is the size of the input array