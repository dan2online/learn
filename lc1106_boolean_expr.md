***1106. Parsing A Boolean Expression***

https://leetcode.com/problems/parsing-a-boolean-expression/

```python
class Solution:
    def parseBoolExpr(self, expression: str) -> bool:
        stack = []
        
        for c in expression:
            if c in ['!', '&', '|', '(', ',']:
                stack.append(c)
            else:
                if c == 'f':
                    stack.append(False)
                elif c == 't':
                    stack.append(True)
                elif c == ')':
                    expr = []
                    while stack:
                        t = stack.pop()
                        if t == '(': break
                        if t == ',': continue
                        if isinstance(t, bool):
                            expr.append(t)
                    if stack:
                        op = stack[-1]
                        if op == '&':
                            res = True
                            for e in expr:
                                res &= e
                        elif op == '|':
                            res = False
                            for e in expr:
                                res |= e
                        elif op == '!':
                            res = not expr[0]
                        stack.pop()
                        stack.append(res)
                    else:
                        stack.append(expr[0])
        return stack[-1] if stack else False
                            
```
