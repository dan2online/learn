***1105. Filling Bookcase Shelves***

https://leetcode.com/problems/filling-bookcase-shelves/

**top-down**

```python
class Solution:
    def minHeightShelves(self, books: List[List[int]], shelf_width: int) -> int:
        n = len(books)
        
        @lru_cache(None)
        def find_min(index: int)->int:
            if index >= n: return 0
            width, height = 0, books[index][1]
            ans = inf
            for i in range(index, n):
                width += books[i][0]
                if width > shelf_width: break
                height = max(height, books[i][1])
                ans = min(ans, height + find_min(i + 1))
            return ans
        
        return find_min(0)
```

**bottom-up**

```python       
class Solution:
    def minHeightShelves(self, books: List[List[int]], shelf_width: int) -> int:
        n = len(books)
        
        dp = [inf] * (n + 1)
        dp[0] = 0
        for i, (width, height) in enumerate(books):
            dp[i+1] = height + dp[i]
            for j in range(i-1, -1, -1):
                width += books[j][0]
                height = max(height, books[j][1])
                if width > shelf_width:
                    break
                dp[i+1] = min(dp[i+1], dp[j] + height)
                
        return dp[n]
 ```
