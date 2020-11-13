



 **1109. Corporate Flight Bookings**

https://leetcode.com/problems/corporate-flight-bookings/submissions/

```python
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        ans = [0] * n
        for i, j, k in bookings:
            for p in range(i, j + 1):
                ans[p-1] += k
        return ans
```


```python
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        q = []
        for i, j, k in bookings:
            heapq.heappush(q, (i, k))
            heapq.heappush(q, (j + 1, -k)) 
        ans, seats = [0]*n, 0
        for i in range(n):
            while q and q[0][0] <= i + 1:
                _, k = heapq.heappop(q)
                seats += k
            ans[i] = seats
        return ans
```

```py
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        ans = [0] * n
        for i, j, k in bookings:
            ans[i - 1] += k
            if j < n: ans[j] -= k
        
        for i in range(1, n):
            ans[i] += ans[i-1]
        return ans
```

<!--Runtime: 828 ms, faster than 93.50% of Python3 online submissions for Corporate Flight Bookings.-->

<!--Memory Usage: 27.8 MB, less than 50.68% of Python3 online submissions for Corporate Flight Bookings.-->

 [similar to lc1094 Car Pooling](lc1094_Car_Pooling.md)

