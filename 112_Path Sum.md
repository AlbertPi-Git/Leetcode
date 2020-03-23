# Leetcode 112 - Path Sum

## Initial idea
Simple DFS, record current sum and compare it with target sum when reaches leaf node. Note that can't do compare in the None node of leaf node because it will make [1,2] satisfy target sum==1.
```python
class Solution:
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        if not root:
            return False
        def dfs(root,Sum):
            if not root.left and not root.right:
                if Sum+root.val==sum:
                    return True
                else:
                    return False
            if root.left:
                if dfs(root.left,Sum+root.val):
                    return True
            if root.right:
                if dfs(root.right,Sum+root.val):
                    return True
            return False
        return dfs(root,0)
```