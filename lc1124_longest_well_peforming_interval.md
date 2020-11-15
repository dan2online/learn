***1124. Longest Well-Performing Interval***

https://leetcode.com/problems/longest-well-performing-interval/



Brute-force (TLE!!!)

```python
class Solution:
    #brute-force TLE!!!
    def longestWPI(self, hours: List[int]) -> int:
        n = len(hours)
        tiring = [0] * (n + 1)
        for i, h in enumerate(hours):
            if h > 8:
                tiring[i + 1] = tiring[i] + 1
            else:
                tiring[i + 1] = tiring[i]
                
        ans = 0
        for i in range(0, n):
            for j in range(1, n + 1):
                tiring_days = tiring[j] - tiring[i]
                non_tiring_days = j - i - tiring_days
                if tiring_days > non_tiring_days:
                    ans = max(ans, j - i)
        return ans
```



Linear scanning (cache)

```python
class Solution:
    def longestWPI(self, hours: List[int]) -> int:
        n = len(hours)
        ans, running = 0, 0
        cache = dict()
        for i in range(n):
            running = running + 1 if hours[i] >8 else running - 1
            # from 0
            if running > 0:
                ans = i + 1
            else:
                if running not in cache:
                    cache[running] = i
                # from running-1: cache[running - 1] to running: i interval meets the req.
                if running - 1 in cache:
                    ans = max(ans, i - cache[running - 1])
        return ans
```

O(n)

https://leetcode.com/problems/longest-well-performing-interval/discuss/396755/Similar-to-Find-the-longest-subarray-with-sum-greater-than-k

> Neutralize the array with 1 and -1.
> If the hours[i] is greater than 8 -> change it to 1
> else change it to -1
>
> Then find the **longest subarray with longest sum greater than k**, where k is set to 0
> Time Complexity : O(nlogn)
> Space Complexity : O(n)

Refs:

https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/

https://www.geeksforgeeks.org/largest-subarray-having-sum-greater-than-k/

