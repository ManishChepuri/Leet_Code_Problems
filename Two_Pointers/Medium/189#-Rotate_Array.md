# Problem 189 - Rotate Array

### Initial Thoughts
- First tried to use a deque as it is O(1) inserting and removing from the start and end but realized the solution would be O(n) space complexity
- Thought about just adding whatever element at the end of the list to the start, but that is O(n) time complexity for adding to the start of a standard python list


### Solution
The trick is to rotate the full array and then just rotate the first k elements and then rotate the remaining elements independently.

Also need to do k mod len(nums) at the start to take care of the case
that k is larger than the length of nums

```
# class Solution:
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k = k % len(nums)
        
        def reverse(l, r):
            while l < r:
                nums[l], nums[r] = nums[r], nums[l]
                l += 1
                r -= 1

        reverse(0, len(nums) - 1)
        reverse(0,  k - 1)
        reverse(k, len(nums) - 1)
```