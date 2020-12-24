***1155. Number of Dice Rolls With Target Sum***



https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/

```python
class Solution:
    def numRollsToTarget(self, d: int, f: int, target: int) -> int:
        
        @lru_cache(None)
        def find_rolls(d, target):
            if d > target or d * f < target:
                return 0
            
            if d == 1: return 1
            
            ans = 0
            for i in range(1, f + 1):
                ans += find_rolls(d - 1, target - i)
            return ans
        
        return find_rolls(d, target) % 1_000_000_007
```



```python
class Solution:          
    def numRollsToTarget(self, d: int, f: int, target: int) -> int:
        if d > target or d * f < target:
            return 0
   
        dp = [[0]*d*f for _ in range(d)]
        for i in range(f):
            dp[0][i]=1
            
        for dice in range(1,d):
            for face in range(dice,(dice+1)*f):
                for b in range(1,f+1):
                    if face-b>=0:
                        dp[dice][face]+=dp[dice-1][face-b]  
                  
        return dp[d-1][target-1]%1_000_000_007
```

