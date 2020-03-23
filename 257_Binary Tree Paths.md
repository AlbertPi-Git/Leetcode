# Leetcode 257 - Binary Tree Paths

## Initial idea
Simple DFS
```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        if not root:
            return []
        res=[]
        def dfs(root,buf):
            if not root.left and not root.right:
                res.append(buf+str(root.val))
            if root.left:
                dfs(root.left,buf+str(root.val)+"->")
            if root.right:
                dfs(root.right,buf+str(root.val)+"->")
        dfs(root,"")
        return res
```