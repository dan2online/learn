**1156. Swap For Longest Repeated Character Substring **

https://leetcode.com/problems/swap-for-longest-repeated-character-substring/



```python
class Solution:
    def maxRepOpt1(self, text: str) -> int:
        max_len, i, n=  0, 0, len(text)
        c, t = collections.Counter(text), collections.defaultdict(lambda :None)
        while i < n:
            j = i
            while i < n - 1 and text[i] == text[i+1]:
                i += 1
            i += 1
            if (i != n or j != 0) and  c[text[j]] > i - j:
                max_len = max(max_len, i - j + 1)
            else:
                max_len = max(max_len, i - j)
                
            if t[text[j]]:
                last = t[text[j]]
                if j - last[1] == 1:
                    if i - last[0] <= c[text[j]]:
                        length = i - last[0]
                    else:
                        length = i - last[0] - 1
                    max_len = max(max_len, length)
            t[text[j]] = (j,i)
        return max_len
```

