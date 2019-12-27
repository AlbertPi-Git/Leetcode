# JianZhi_12 Binary Tree BFS

## Initial idea
Simple BFS
```python
from collections import deque
class Solution:
    def PrintFromTopToBottom(self, root):
        res=[]
        dQ=deque()
        if root:
            dQ.append(root)
        while dQ:
            front=dQ.popleft()
            res.append(front.val)
            if front.left:
                dQ.append(front.left)
            if front.right:
                dQ.append(front.right)
        return res
```