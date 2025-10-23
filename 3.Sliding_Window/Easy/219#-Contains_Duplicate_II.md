# Problem 219 - Contains Duplicate II

## Initial Thoughts
- Initialize a set with the first k + 1 elements
- Check if len(set) is less than k + 1. If so then return True since there is a duplicate
- If not, then make a sliding window. Remove left index from set, and increment left. Then incremeent right and try to add that element to set. If the len(set) < k + 1 then return True, else repeat process.

## Solution

### First Attempt
```
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        if len(nums`) == 0:
            return False

        k = min(len(nums) - 1, k)
        unique_nums = set()
        l = 0

        for r in range(0, len(nums)):
            if r > k:
                unique_nums.remove(nums[l])
                l += 1
            unique_nums.add(nums[r])
            if len(unique_nums) < r - l + 1: return True

        return False
```
SOLVED