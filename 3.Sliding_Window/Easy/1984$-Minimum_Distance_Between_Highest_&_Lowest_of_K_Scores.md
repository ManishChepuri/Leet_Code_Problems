# Problem 1984 - Minimum Distance Between Highest & Lowest of K Scores

### Initial Thoughts
- First though about trying sliding window. Sort the array first and then thought about how to apply sliding
window but couldn't figure it out.
- Then thought about using two pointers. First you would sort the array. Then, l would start at the left and r would start at the right of the array.Then whichever had the greatest abs() of the next num would be incremented/decremented. Keep repeating while l < r.
- I forgot about the k variable. The problem is saying that you HAVE to choose k students so that the difference between the highest and lowest of those k students is minimized. Meaning that if the problem said 7 students and there were two numbers 99, and 100 in the nums array, the minimized difference couldn't be 1 because there are probably numbers less than 99 that you would have to include.
- Go back to sliding window strategy. First sort the numbers, then use a sliding window of two pointers of size 7 to slide across nums. Keep calculating the difference between the rightmost and leftmost element until you get to the end where you return the minimum.

## Solution

### First Attempt
```
class Solution:
    def minimumDifference(self, nums: List[int], k: int) -> int:
        nums.sort()
        l = 0
        min_distance = nums[len(nums) - 1] - nums[0]
        for r in range(k - 1, len(nums)):
            min_distance = min(min_distance, nums[r] - nums[l])
            l += 1

        return min_distance
```
SOLVED
