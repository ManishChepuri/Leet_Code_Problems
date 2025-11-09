# Problem 153 - Find Minimum in Rotated Sorted Array


## Solution
* Watched NeetCode video to learn how think in the way to solve these problems. Coded solution on my own.
- This problem is kinda tricky. First since its saying that the solution must be in O(logn) time, and we are searching for a minimum element, it would be a good idea to try to use binary search. If we think about normal binary search if the input array was not rotated and we were searching for a specific element, we would start at the middle of the array and see if that element is greater than or less than our desired element move to the left or right depending on that.
- This problem is a bit different though since the input array is rotated. The trick to solve this problem revolves around the fact all elements to the right of the pivot point (which is the end of the original array and the start of the rotated elements) are **ALL** less than every element to the left of the pivot point. What this means is that once you establish your first Left, Right, and Middle pointer, if the Right pointer is less than the Left pointer, then you must find out if your Middle pointer is in the unrotated or rotated side of the array. If the Middle pointer is greater than the element at the Left pointer, then the Middle pointer is in the unrotated side of the array. Then you move the Left pointer to the element to the right of the Middle pointer. If the Middle pointer is less than the Left pointer, then the Middle pointer is in the rotated side of the array. Then you move the Right pointer to the element to the left of the Middle pointer. You keep repeating this until the Left pointer is less than the Right pointer which means that both pointers are in the rotated side of the array. and you can return the Left pointer if its less than the current minimum element (forgot to mention that during this whole process the applicants for the minimum element is the element at the Middle pointer).

### First Attempt
```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l = 0
        r = len(nums) - 1
        m = r // 2 + 1
        minimum = nums[m]

        print(m)
        while r < l:
            if nums[m] >= nums[l]:
                l = m + 1
            else:
                r = m - 1
            minimum = min(nums[m], minimum)

        return min(nums[l], minimum)
```

### Second Attempt
```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        if len(nums) == 1: return nums[0]
        l = 0
        r = len(nums) - 1
        m = r // 2
        minimum = nums[m]

        print(m)
        while r < l:
            if nums[m] >= nums[l]:
                l = m + 1
            else:
                r = m - 1
            minimum = min(nums[m], minimum)

        return min(nums[l], minimum)
```

### Last Attempt
```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        if len(nums) == 1: return nums[0]
        l = 0
        r = len(nums) - 1
        m = r // 2
        minimum = nums[m]

        print(m)
        while nums[r] < nums[l]:
            if nums[m] >= nums[l]:
                l = m + 1
            else:
                r = m - 1
            m = (r + l) // 2
            minimum = min(nums[m], minimum)

        return min(nums[l], minimum)
```
SOLVED
- Time Complexity: O(logn)
    - Used Binary Search
- Space Complexity: O(1)
    - Did not create any more data structures that grew in size as the input array grew in size