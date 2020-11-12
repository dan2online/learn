***1095. Find in Mountain Array***

https://leetcode.com/problems/find-in-mountain-array/

```python
# """
# This is MountainArray's API interface.
# You should not implement it, or speculate about its implementation
# """
#class MountainArray:
#    def get(self, index: int) -> int:
#    def length(self) -> int:

class Solution:
    def findInMountainArray(self, target: int, mountain_arr: 'MountainArray') -> int:

        def find_target(lo, hi, bound):
            if hi >= bound: hi = bound - 1
            if lo > hi or lo > bound:
                return inf
            
            mid = lo + (hi - lo)//2            
            a = mountain_arr.get(mid)
            if a == target:
                return min(mid, find_target(lo, mid -1, min(mid, bound)))
            
            if mid < hi:
                b = mountain_arr.get(mid + 1)
                if a < b:
                    # ascending
                    if a < target:
                        return find_target(mid + 1, hi, bound)
                    return find_target(lo, mid - 1, bound)
                else:
                    # descending
                    if a < target:
                        return find_target(lo, mid - 1, bound)
                    return min(find_target(mid + 1, hi, bound), find_target(lo, mid - 1, bound))
            return find_target(lo, mid - 1, bound)

        ans = find_target(0, mountain_arr.length() - 1, inf)
        return -1 if ans == inf else ans
        
```

***Triple binary search***

https://leetcode.com/problems/find-in-mountain-array/discuss/928558/Divide-and-conquer-Simple-stategy

* Step 1 - Identify the mountain peak (using binary search)
* Step 2 - Divide the mountain into ascending and descending slopes : 0...PEAK and PEAK....N
* Step 3 - Perform binary search on ascending first, and then descending slope.

Runtime - LogN

