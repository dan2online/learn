**1128. Number of Equivalent Domino Pairs **

https://leetcode.com/problems/number-of-equivalent-domino-pairs/

```python
class Solution:
    def numEquivDominoPairs(self, dominoes: List[List[int]]) -> int:
        d = dict()
        for a, b in  dominoes:
            a, b = min(a, b), max(a, b)
            if (a, b) in d:
                d[(a, b)] += 1
            else:
                d[(a, b)] = 1
        
        ans = 0
        for _, n in d.items():
            ans += (n - 1) * n//2
        return ans
```

