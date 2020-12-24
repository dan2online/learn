

***1147. Longest Chunked Palindrome Decomposition***

https://leetcode.com/problems/longest-chunked-palindrome-decomposition/

```python
class Solution:
    def longestDecomposition(self, text: str) -> int:
        n = len(text)
        
        def find_p(i, j):
            if i > j:
                return 0
            
            k = j
            while i <= k:
                while i <= k and text[k] != text[i]:
                    k -= 1
             
                m = j - k + 1
                if text[i : i + m] == text[k : k + m]:
                    break
                k -= 1
                
            if i == k: return 1
            
            return 2 + find_p(i + j - k + 1, k - 1)
                
        return find_p(0, n - 1)
```



https://leetcode.com/problems/longest-chunked-palindrome-decomposition/discuss/897806/python-3-look-for-smallest-subtext-that-matches-at-beginning-and-end-(if-any)-and-recurse

```python
class Solution:
    def longestDecomposition(self, text: str) -> int:
        n = len(text)
        if n <= 1: return n
        for i in range(1,n//2+1):
            if text[:i] == text[-i:]:
                return 2+self.longestDecomposition(text[i:-i])
        return 1
```

