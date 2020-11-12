***1104. Path In Zigzag Labelled Binary Tree***

https://leetcode.com/problems/path-in-zigzag-labelled-binary-tree/

```python
class Solution:
    def pathInZigZagTree(self, label: int) -> List[int]:
        ans, num = [], 1<<32
        for k in range(32, -1, -1):
            if label >= num:
                ans.append(label)
                #print(f'k = {k} num={num} label={label}')
                if k % 2:
                    pos = num * 2 - 1 - label
                    label = (num >> 1) + pos//2
                else:
                    pos = label - num
                    label = num - 1 - pos//2
            num >>= 1
        return reversed(ans)
                
```
