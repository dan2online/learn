***1094. Car Pooling***

https://leetcode.com/problems/car-pooling/

**Brute force**

```python
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        trip_num = [0] * 1001
        for num, start, end in trips:
            for i in range(start, end):
                trip_num[i] += num
        max_num = max(trip_num)
        return max_num <= capacity
```


```python
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        trip_num = [0] * 1001
        for num, start, end in trips:
            trip_num[start] += num
            trip_num[end] -= num
         
        needed = 0
        for num in trip_num:
            needed += num
            if needed > capacity: return False
        return True
```

**priority queue**

```python
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        q = []
        for num, start, end in trips:
            heapq.heappush(q, (start, num))
            heapq.heappush(q, (end, -num))
        
        cur = 0
        while q:
            _, num = heapq.heappop(q)
            cur += num
            if cur > capacity: return False
        return True
            
```
