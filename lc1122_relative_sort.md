***1122. Relative Sort Array***

https://leetcode.com/problems/relative-sort-array/

```python
class Solution:
    def relativeSortArray(self, arr1: List[int], arr2: List[int]) -> List[int]:
        res = [0] * 1001
        for a in arr1:
            res[a] += 1
        
        ans = []
        for a in arr2:
            if res[a]:
                ans += [a] * res[a]
            res[a] = 0
            
        for a, k in enumerate(res):
            if k: ans += [a] * k
                
        return ans
```

