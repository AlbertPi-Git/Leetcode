# Leetcode 429 - N-ary Tree Level Order Traversal

## Initial idea
Simply use queue
```python
from collections import deque
class Solution:
    def levelOrder(self, root: 'Node') -> List[List[int]]:
        res=[]
        Q=deque([[root]]) if root else deque()
        while Q:
            frontLevel=Q.popleft()
            res.append([node.val for node in frontLevel])
            nextLevel=[]
            for node in frontLevel:
                for child in node.children:
                    nextLevel.append(child)
            if nextLevel:
                Q.append(nextLevel)
        return res
```