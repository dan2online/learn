

***1143. Longest Common Subsequence***

1. Top-down memorization

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n, m = len(text1), len(text2)
        
        @lru_cache(None)
        def find_lcs(i, j):
            if i == n or j == m:
                return 0
            
            if text1[i] == text2[j]:
                return 1 + find_lcs(i + 1, j + 1)
        
            return max(find_lcs(i + 1, j), find_lcs(i, j + 1))
        return find_lcs(0, 0)
        
        return find_lcs(0, 0)
    
```

2. DP - 2D

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[0]*(n+1) for _ in range(m + 1)] 
        
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i-1] == text2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j-1], dp[i-1][j], dp[i][j-1])
        return dp[m][n]
```

3. DP - 1D

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[0]*(n+1) for _ in range(2)] 
        
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i-1] == text2[j-1]:
                    dp[i%2][j] = dp[(i-1)%2][j-1] + 1
                else:
                    dp[i%2][j] = max(dp[(i-1)%2][j], dp[i%2][j-1])
        return dp[m%2][n]
```



