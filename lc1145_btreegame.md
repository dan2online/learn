

***1145. Binary Tree Coloring Game***

https://leetcode.com/problems/binary-tree-coloring-game/

Answer from https://leetcode.com/problems/binary-tree-coloring-game/discuss/824348/Python3-basic-DFS

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def btreeGameWinningMove(self, root: TreeNode, n: int, x: int) -> bool:
        candidates = []

        def dfs(curr):
            if not curr:
                return 0

            l = dfs(curr.left)
            r = dfs(curr.right)

            if curr.val == x:
                l and candidates.append(l) # X's left subtree is a candidate
                r and candidates.append(r) # X's right subtree is a candidate

            return 1 + l + r

        dfs(root)

        # Last candidate: total - (X and its subtrees)
        candidates.append(n - sum(candidates) - 1)

        # Find a candidate where I can win
        return any(mine > n - mine for mine in candidates)
```



<img src="https://assets.leetcode.com/uploads/2019/08/01/1480-binary-tree-coloring-game.png" alt="img" style="zoom:50%;" />

> Count left and right children's nodes of the player 1's initial node with value x. Lets call countLeft and countRight.
>
> 
>
> if countLeft or countRight are bigger than n/2, player 2 chooses this child of the node and will win.
> If countLeft + countRight + 1 is smaller than n/2, player 2 chooses the parent of the node and will win;
> otherwise, player 2 has not chance to win.