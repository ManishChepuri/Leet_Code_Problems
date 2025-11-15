# Problem 981 - Time Based Key-Value Store

## Solution
- This problem you have to mix using a hashmap with binary search to find the correct timestamp in the most efficient way
- The set method is pretty easy as you just add the element to the hashmap with the value being a tuple of (value, timestamp)
- for the get method, its a bit more complicated. You must first see if the inputted key is even in the hashmap. If it is, you have to run binary search until you get to a point where either the desired timestamp is found in the hashmap or if you get to a point where the timestamp is between a timestamp less than it and greater than it.

### First Attempt
```
class TimeMap:

    def __init__(self):
        self.timemap = defaultdict(list) # key : List((value, time))

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.timemap[key].append((value, timestamp))

    def get(self, key: str, timestamp: int) -> str:
        values = self.timemap.get(key, None)
        if values == None:
            return None
        l = 0
        r = len(values) - 1
        m = (l + r) // 2

        while l < r:
            if values[m][1] > timestamp:
                r = m - 1
            elif values[m][1] < timestamp:
                l = m + 1
            m = (l + r) // 2
        
        return values[m][0]



# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```

- After this attempt I realized I had to implement the feature where the timestamp doesn't have to be exactly found in the list

### Second Attempt
```
class TimeMap:

    def __init__(self):
        self.timemap = defaultdict(list) # key : list of (value, timestamp)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.timemap[key].append((value, timestamp))

    def get(self, key: str, timestamp: int) -> str:
        values = self.timemap.get(key, [])
        if len(values) == 0:
            return ""

        l, r = 0, len(values) - 1
        m = (l + r) // 2

        if timestamp < values[0][1]:
            return ""
        if timestamp > values[-1][1]:
            return values[-1][0]

        while l < r:
            if timestamp < values[m][1]:
                if timestamp > values[m - 1][1]:
                    return values[m - 1][0]
                r = m - 1
            elif timestamp > values[m][1]:
                if timestamp < values[m + 1][1]:
                    return values[m][0]
                l = m + 1
            else:
                return values[m][0]

            m = (l + r) // 2
        

        return values[m][0]



# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)
```
SOLVED
- Time Complexity = O(1) for set and O(log*n*) for get
- Space Complexity = O(*n*)


### Post Thoughts
- My solution was not as simple and could be made more simple. Instead of adding the feature to check if the timestamp is greater than one element and less than the next to return, I could have just set the timestamp to return the value from equal to the return timestamp and if during the binary search I found a timestamp greater than that one I would use the new one. At the end I would just return whatever the value is from greatest timestamp I found that is less than the desired timestamp.