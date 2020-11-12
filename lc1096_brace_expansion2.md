***1096. Brace Expansion II***

https://leetcode.com/problems/brace-expansion-ii/

simiar to calculator using stack

```python
class Solution:
    def braceExpansionII(self, expression: str) -> List[str]:
        stack = []
        for c in expression:
            if c == '{' or c == ',':
                stack.append(c)
            elif c == '}':
                s = set()
                while stack:
                    t = stack.pop()
                    if t == '{': break
                    if t == ',': continue
                    s |= t
                    
                if not stack or stack[-1] == '{' or stack[-1] == ',':
                    stack.append(s)
                else:
                    # merge
                    new_s = set()
                    if isinstance(stack[-1], set):
                        for s1 in stack.pop():
                            for s2 in s:
                                new_s.add(s1 + s2)
                    stack.append(new_s)
            else:
                if not stack or stack[-1] == '{' or stack[-1] == ',':
                    stack.append({c})
                else:
                    if isinstance(stack[-1], set):
                        s = set()
                        for v in stack.pop():
                            s.add(v + c)
                        stack.append(s)
        #print(f'{stack}')
        return sorted(list(stack.pop()))
        
```
