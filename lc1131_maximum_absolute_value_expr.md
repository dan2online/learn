

**1131. Maximum of Absolute Value Expression**


https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/

* Brute-force (TLE!!!)

  ```python
  class Solution1:
      def maxAbsValExpr(self, arr1: List[int], arr2: List[int]) -> int:
          n = len(arr1)
          ans  = 0
          for i in range(n):
              for j in range(n):
                  ans = max(ans,
                            abs(arr1[i] - arr1[j]) + 
                            abs(arr2[i] - arr2[j]) +
                            abs(i - j))
          return ans
  ```

  - Time Limit Exceeded

* 4-scenarios

  ```python
  class Solution:
      def maxAbsValExpr(self, arr1: List[int], arr2: List[int]) -> int:
          '''
          |arr1[i] - arr1[j]| + |arr1[i] + arr2[j]| + |i - j|
          ==>
           (arr1[i] - arr1[j]) + (arr2[i] - arr2[j]) + (i - j)
           (arr1[i] - arr1[j]) - (arr2[i] - arr2[j]) + (i - j)
          -(arr1[i] - arr1[j]) + (arr2[i] - arr2[j]) + (i - j)
          -(arr1[i] - arr1[j]) - (arr2[i] - arr2[j]) + (i - j)
          ==>
          (arr1[i]  + arr2[i] + i) - (arr1[j]  + arr2[j] + j)
          (arr1[i]  - arr2[i] + i) - (arr1[j]  - arr2[j] + j)
          (-arr1[i] + arr2[i] + i) - (-arr1[j] + arr2[j] + j)
          (-arr1[i] - arr2[i] + i) - (-arr1[j] - arr2[j] + j)
          '''
          n = len(arr1)
          ans = -inf
          for sign1, sign2 in [(1, 1), (1, -1), (-1, 1), (-1, -1)]:
              min_a, max_a = inf, -inf
              for i in range(n):
                  a = arr1[i] * sign1 + arr2[i] * sign2 + i
                  max_a = max(max_a, a)
                  min_a = min(min_a, a)
              ans = max(ans, max_a - min_a)
          return ans
              
  ```

  - Runtime: 344 ms, faster than 67.50% of Python3 online submissions for Maximum of Absolute Value Expression.

  - Memory Usage: 21 MB, less than 83.13% of Python3 online submissions for Maximum of Absolute Value Expression.

