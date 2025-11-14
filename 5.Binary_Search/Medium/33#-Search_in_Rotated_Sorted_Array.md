# Problem 33 - Search in Rotated Sorted Array

## Solution

### Initial Thoughts
- This one is similar to Problem 153 - Find Minimum in Rotated Sorted Array
- A necessary fact to understand about this problem to complete it is that every element to the left of the pivot point (which is the point where the array switches from the greatest element to the smallest element) is all greater than nums[0] and everything to the right of the pivot point is less than nums[0]. Then the first step you need to do is find if the target value is in the right or left side of the pivot point. Depending on the side of the target value that is the side you need to search. You then need to initialize the middle pointer and then incremenet the necessary right or left pointer to move the middle to the side of the target. Then you need to keep doing binary search until you end up at the target.

### First Attempt
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0
        r = len(nums) - 1
        m = (l + r) // 2
        
        if nums[m] == target: # If m is initially at target just return m
            return m

        if target < nums[0]: # Search right side of pivot
            while l < r:
                if nums[m] < nums[0]: # middle is right of pivot
                    if target < nums[m]: # target is left of middle
                        r = m - 1
                    elif target > nums[m]: # target is right of middle
                        l = m + 1
                    else:
                        return m
                else: # middle is left of pivot
                    l = m + 1
                m  = (l + r) // 2
            if nums[m] == target:
                return m
            else:
                return -1
        elif target > nums[0]: # Search left side of the pivot
            while l < r:
                if nums[m] >= nums[0]: # Middle is left of the pivot
                    if target < nums[m]: # Target is left of middle
                        r = m - 1
                    elif target > nums[m]: # Target is right of middle
                        l = m + 1
                    else:
                        return m
                else: # Middle is right of the pivot
                    r = m - 1
                m = (l + r) // 2
            if nums[m] == target:
                return m
            else:
                return -1
        else:
            return nums[0]
```

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0
        r = len(nums) - 1
        m = (l + r) // 2
        
        if nums[m] == target: # If m is initially at target just return m
            return m

        if target < nums[0]: # Search right side of pivot
            while l < r:
                if nums[m] < nums[0]: # middle is right of pivot
                    if target < nums[m]: # target is left of middle
                        r = m - 1
                    elif target > nums[m]: # target is right of middle
                        l = m + 1
                    else:
                        return m
                else: # middle is left of pivot
                    l = m + 1
                m  = (l + r) // 2
            if nums[m] == target:
                return m
            else:
                return -1
        elif target > nums[0]: # Search left side of the pivot
            while l < r:
                if nums[m] >= nums[0]: # Middle is left of the pivot
                    if target < nums[m]: # Target is left of middle
                        r = m - 1
                    elif target > nums[m]: # Target is right of middle
                        l = m + 1
                    else:
                        return m
                else: # Middle is right of the pivot
                    r = m - 1
                m = (l + r) // 2
            if nums[m] == target:
                return m
            else:
                return -1
        else:
            return 0
```