**1138. Alphabet Board Path**

https://leetcode.com/problems/alphabet-board-path/

```python
class Solution:
    def alphabetBoardPath(self, target: str) -> str:
        prev_r, prev_c = 0, 0
        ans = ''
        for a in target:
            i = ord(a) - ord('a')
            r, c = (i//5, i%5)
            if r == 5 and prev_r != 5:
                choices = [(4, c), (5, c)]
            else:
                choices = [(r, c)]

            for r, c in choices:
                if r > prev_r:
                    ans += 'D'*(r - prev_r)
                elif r < prev_r:
                    ans += 'U'*(prev_r - r)
                if c > prev_c:
                    ans += 'R' * (c - prev_c)
                elif c < prev_c:
                    ans += 'L' * (prev_c - c)
                prev_r, prev_c = r, c
            ans += '!'
        return ans
```

<img src="https://assets.leetcode.com/uploads/2019/07/28/azboard.png" alt="img" style="zoom:50%;" />

