# Problem 11 | Container With Most Water

### Initial thoughts
* Picking two bars, the maximum amount of water they can hold is just the width * min(left_bar, rigth_bar).
* Only way to gain water is if the smaller/limiting bar were to move to a larger bar
* Start left pointer at `0` and the right pointer at `len(height) - 1`

* First thoughts was to move to the next largest area but then that would miss out on keeping your pointer on a large bar.
* Try moving only the smaller pointer to the next one

### First Solution
```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        max_water = 0
        l, r = 0, len(height) - 1
        while l < r:
            water = (r - l) * min(height[l], height[r])
            max_water = max(max_water, water)
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return max_water
```

SOLVED
