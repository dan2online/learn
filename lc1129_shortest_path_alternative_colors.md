**1129. Shortest Path with Alternating Colors **

https://leetcode.com/problems/shortest-path-with-alternating-colors/



```python
class Solution:
    def shortestAlternatingPaths(self, n: int, red_edges: List[List[int]], blue_edges: List[List[int]]) -> List[int]:
        g = dict()
        for i, edges in enumerate([red_edges, blue_edges]):
            for u, v in edges:
                if u not in g:
                    g[u] = [[], []]
                g[u][i].append(v)    
 
        RED, BLUE = 0, 1
        ans = [inf] * n
        q = deque([(0, RED, 0),(0, BLUE, 0)])
        visited = set()
        while q:
            for _ in range(len(q)):
                node, color, dist = q.popleft()
                if (node, color) in visited:
                    continue
                visited.add((node, color))
                ans[node] = min(ans[node], dist)
                if node in g:
                    color = RED if color == BLUE else BLUE
                    for v in g[node][color]:
                        if (v, color) not in visited:
                            q.append((v, color, dist + 1))
        ans = [ -1 if x == inf else x for x in ans ]
        return ans
```