**1139. Largest 1-Bordered Square**

https://leetcode.com/problems/largest-1-bordered-square/

- Brute-force

```python
class Solution:
    def largest1BorderedSquare(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        
        def find_max_square(top, left, bottom, right):
            for i in range(top, bottom + 1):
                if not grid[i][left]: return 0
                if not grid[i][right]: return 0
            for i in range(left, right + 1):
                if not grid[top][i]: return 0
                if not grid[bottom][i]: return 0
            return bottom - top + 1
        
        ans = 0
        for i in range(m):
            for j in range(n):
                if not grid[i][j]: continue
                max_side = min(m - i, n - j)
                if ans >= max_side: break
                for side in range(max_side - 1, -1, -1):
                    ans = max(ans, find_max_square(i, j, i + side, j + side))
                        
        return ans * ans
```

- Dynamic programing (O(n^3))

```python
    
class Solution:
    def largest1BorderedSquare(self, grid: List[List[int]]):
        m, n = len(grid), len(grid[0])
        hmat = [[0]*n for _ in range(m)]
        vmat = [[0]*n for _ in range(m)]
        
        ans = 0
        for i in range(m):
            for j in range(n):
                if i==0:
                    vmat[i][j] = grid[i][j]
                elif grid[i][j]:
                    vmat[i][j] = vmat[i-1][j] +1
                else:
                    vmat[i][j] = 0
 
                if j==0:
                    hmat[i][j] = grid[i][j]
                elif grid[i][j]:
                    hmat[i][j] = hmat[i][j-1]+1 
                else:
                    hmat[i][j] = 0
        
        for i in range(m-1, -1, -1):
            for j in range(n-1, -1, -1):
                if i+1 <= ans or j+1 <= ans: break
                
                maxside = min(hmat[i][j], vmat[i][j])  
                for w in range(maxside, -1, -1):
                    if w <= ans: break
         
                    if hmat[i-(w-1)][j] >= w and vmat[i][j-(w-1)] >= w:
                        ans = max(ans, w)
                        break      
        return ans*ans
```

