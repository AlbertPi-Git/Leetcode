# JianZhi_12 Mirror Binary Tree

## Initial idea
Simple recursion
```python
class Solution:
    def Mirror(self, root):
        if not root:
            return
        leftTmp=root.left
        rightTmp=root.right
        root.left=rightTmp
        root.right=leftTmp
        self.Mirror(leftTmp)
        self.Mirror(rightTmp)
        return root
```