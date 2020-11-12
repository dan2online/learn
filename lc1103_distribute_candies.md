***1103. Distribute Candies to People***

https://leetcode.com/problems/distribute-candies-to-people/

```python
class Solution:
    def distributeCandies(self, candies: int, num_people: int) -> List[int]:
        ans, k = [0] * num_people, 0
        
        while candies:
            for i in range(num_people):
                needed = k * num_people + i + 1
                if needed <= candies:
                    ans[i] += needed
                    candies -= needed
                else:
                    ans[i] += candies
                    candies = 0
                    break
            k += 1
        return ans
  ```
