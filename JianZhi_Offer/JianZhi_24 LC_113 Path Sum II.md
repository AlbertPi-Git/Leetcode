# JianZhi_24 LC_113 - Path Sum II

## Initial idea
DFS, record path and sum, verify and append to res at leaf node. Since it requires longer list is in the front of res, so to tuple to record length of list and sort.

```python
class Solution:
    def FindPath(self, root, expectNumber):
        if not root:
            return []
        res=[]
        def dfs(root,path,Sum):
            if not root.left and not root.right:
                if Sum+root.val==expectNumber:
                    res.append((len(path+[root.val]),path+[root.val]))
                return
            if root.left:
                dfs(root.left,path+[root.val],Sum+root.val)
            if root.right:
                dfs(root.right,path+[root.val],Sum+root.val)
        dfs(root,[],0)
        res.sort(reverse=True)
        res=[item[1] for item in res]
        return res
```

## LC 113
Doesn't require the order, so simple list[list] is enough.
```python
class Solution:
    def pathSum(self, root: TreeNode, expectNumber: int) -> List[List[int]]:
        if not root:
            return []
        res=[]
        def dfs(root,path,Sum):
            if not root.left and not root.right:
                if Sum+root.val==expectNumber:
                    res.append(path+[root.val])
                return
            if root.left:
                dfs(root.left,path+[root.val],Sum+root.val)
            if root.right:
                dfs(root.right,path+[root.val],Sum+root.val)
        dfs(root,[],0)
        return res
```