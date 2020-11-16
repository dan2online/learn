**1130. Minimum Cost Tree From Leaf Values**

https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/

- Top-down DFS + memorization (O(n^3))

```python
class Solution:
    def mctFromLeafValues(self, arr: List[int]) -> int:
        @lru_cache(None)
        def find_root_node(lo, hi):
            if lo == hi: return 0
            if hi - lo == 1: return arr[lo] * arr[hi]
            ans = inf
            for i in range(lo, hi):
                ans = min(ans,
                          max(arr[lo : i+1]) * max(arr[i+1:hi + 1]) + 
                          find_root_node(lo, i) +
                          find_root_node(i + 1, hi))
            return ans
        return find_root_node(0, len(arr) - 1)
```

* Dynamic programing (O(n^3))

  ```python
  class Solution:
      def mctFromLeafValues(self, arr: List[int]) -> int:
          n = len(arr)
          dp = [[ inf ] * n for _ in range(n)]
          
          for i in range(n):
              dp[i][i]=0
          for i in range(0, n-1):
              dp[i][i+1] = arr[i] * arr[i+1]
       
          for d in range(2, n + 1):
              for lo in range(0, n - d):
                  hi = lo + d
                  for i in range(lo, hi):
                      dp[lo][hi] = min(dp[lo][hi], max(arr[lo : i + 1]) * max(arr[i + 1: hi+1]) + 
                                   dp[lo][i] + 
                                   dp[i+1][hi])
          return dp[0][-1]
  ```

* Greedy algorithm
  $$
  O(n^2)
  $$

  ```python
  class Solution:
      def mctFromLeafValues(self, arr: List[int]) -> int:
          ans = 0
          while len(arr) > 1:
              i = arr.index(min(arr))
              # recall: 0 or 2 leaf nodes
              if i == 0:
                  ans += arr[i] * arr[i+1]
              elif i == len(arr)-1:
                  ans += arr[i] * arr[i-1]
              else:
                  ans += arr[i] * min(arr[i+1], arr[i-1])
              arr.pop(i) 
          return ans
  ```

* Stack ( O(N) O(N))

  ```python
  class Solution:
      def mctFromLeafValues(self, arr: List[int]) -> int:
          ans = 0
          stack = [inf]
          for num in arr:
              #print(f'stack={stack} num={num}')
              # remove all local minimums
              while stack and num >= stack[-1]: 
                  ans += stack.pop() * min(stack[-1], num)
              stack.append(num)
              #print(f'ans = {ans}')
          while len(stack) > 2:
              #print(f'stack={stack}')
              ans += stack.pop() * stack[-1]
              #print(f'ans = {ans}')
          return ans
  ```

       ```tex
Your input
[6,2,4,1,2,3,4,5,6,5,4,3,2,6,7]

stack=[inf] num=6
ans = 0
stack=[inf, 6] num=2
ans = 0
stack=[inf, 6, 2] num=4
ans = 8
stack=[inf, 6, 4] num=1
ans = 8
stack=[inf, 6, 4, 1] num=2
ans = 10
stack=[inf, 6, 4, 2] num=3
ans = 16
stack=[inf, 6, 4, 3] num=4
ans = 44
stack=[inf, 6, 4] num=5
ans = 64
stack=[inf, 6, 5] num=6
ans = 130
stack=[inf, 6] num=5
ans = 130
stack=[inf, 6, 5] num=4
ans = 130
stack=[inf, 6, 5, 4] num=3
ans = 130
stack=[inf, 6, 5, 4, 3] num=2
ans = 130
stack=[inf, 6, 5, 4, 3, 2] num=6
ans = 234
stack=[inf, 6] num=7
ans = 276
       ```

* References

  https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/847108/DP-matrix-Chain-Multiplication-with-comments-and-reference

  Greedy algorithm ?

  https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/679197/Summary-of-the-3-main-solutions-concise-yet-clear-python

  





