

***1144. Decrease Elements To Make Array Zigzag***

two-pass greedy 

```python
class Solution:
    def movesToMakeZigzag(self, nums: List[int]) -> int:
        n = len(nums)
        ans = inf
        for inc in [True, False]:
            res = [ num for num in nums]
            moves = 0
            for i in range(1, n):
                if inc:
                    if res[i - 1] >= res[i]:
                        moves += res[i - 1] - res[i] + 1
                        res[i - 1] = res[i] - 1
                else:
                    if res[i - 1] <= res[i]:
                        moves += res[i] - res[i-1] +1
                        res[i] = res[i - 1] - 1
                inc = not inc
            ans = min(moves, ans)
        return ans
```

