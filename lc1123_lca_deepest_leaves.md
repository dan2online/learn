***1123. Lowest Common Ancestor of Deepest Leaves***

https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def lcaDeepestLeaves(self, root: TreeNode) -> TreeNode:
    
        @lru_cache(None)
        def find_max_depth(node: TreeNode)->int:
            if not node: return 0
            return 1 + max(find_max_depth(node.left), find_max_depth(node.right))
        
        def find_lca(node: TreeNode)->TreeNode:
            if not node: return None
            left_depth = find_max_depth(node.left)
            right_depth = find_max_depth(node.right)
            if left_depth >right_depth:
                return find_lca(node.left)
            if left_depth < right_depth:
                return find_lca(node.right)
            return node
        
        return find_lca(root)
```

- post-order

```python
class Solution:
    def lcaDeepestLeaves(self, root: TreeNode) -> TreeNode:
        
        def find_lca(node: TreeNode):
            if not node: return (0, None)
            left_depth, left_node = find_lca(node.left)
            right_depth, right_node = find_lca(node.right)
            if left_depth == right_depth:
                return (left_depth + 1, node)
            if left_depth > right_depth:
                return (left_depth + 1, left_node)
            return (right_depth + 1, right_node)
        
        _, ans = find_lca(root)
        return ans
```

