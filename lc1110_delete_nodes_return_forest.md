***1110. Delete Nodes And Return Forest***

https://leetcode.com/problems/delete-nodes-and-return-forest/

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def delNodes(self, root: TreeNode, to_delete: List[int]) -> List[TreeNode]:
        node_dict = dict()
        
        def gen_node_map(node: TreeNode, parent: TreeNode):
            if not node: return
            node_dict[node.val] = [node, parent]
            gen_node_map(node.left, node)
            gen_node_map(node.right, node)
        
        gen_node_map(root, None)
        for v in to_delete:
            del node_dict[v]

        ans = []
        for k, ni in node_dict.items():
            node, parent = ni
            if parent and parent.val not in node_dict:
                parent = None
            if node.left and node.left.val not in node_dict:
                node.left = None
            if node.right and node.right.val not in node_dict:
                node.right = None
        
            if not parent:
                ans.append(node)
        return  ans
```

