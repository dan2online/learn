***1096. Brace Expansion II***

https://leetcode.com/problems/brace-expansion-ii/

simiar to calculator using stack

```python
class Solution:
    def braceExpansionII(self, expression: str) -> List[str]:
        
        def set_product(s1:set, s2:set)->set:
            return set([ i + j for i in s1 for j in s2])
                       
        stack = []
        for c in expression:
            if c == '{' or c == ',':
                stack.append(c)
            elif c == '}':
                #union
                s = set()
                while stack:
                    t = stack.pop()
                    if t == '{': break
                    if t == ',': continue
                    s |= t
                   
                if not stack or stack[-1] == '{' or stack[-1] == ',':
                    stack.append(s)
                elif isinstance(stack[-1], set):
                    stack.append(set_product(stack.pop(), s))
            else:
                if not stack or stack[-1] == '{' or stack[-1] == ',':
                    stack.append({c})
                elif isinstance(stack[-1], set):
                    stack.append(set_product(stack.pop(), {c}))
        #print(f'{stack}')
        return sorted(list(stack.pop()))
        
```
