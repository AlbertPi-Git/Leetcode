# Leetcode 101 - Symmetric Tree

## Initial idea 1
Generate serialized left tree and right tree recursively then compare. DFS left and right in opposite order in two functions.
```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        def Traversal_left(root):
            if not root:
                return [None]
            return [root.val]+Traversal_left(root.left)+Traversal_left(root.right)
        
        def Traversal_right(root):
            if not root:
                return [None]
            return [root.val]+Traversal_right(root.right)+Traversal_right(root.left)
        
        return Traversal_left(root.left)==Traversal_right(root.right)
```

## Initial idea 2
Compare left tree and right tree iteratively using two stacks. Put left and right to stack in opposite order in two stacks.
```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        if not root:
            return True
        stack1,stack2=[root.left],[root.right]
        while stack1 and stack2:
            top1,top2=stack1.pop(),stack2.pop()
            if not top1 and not top2:
                continue
            if not top1 or not top2:
                return False
            if top1.val==top2.val:
                stack1.append(top1.left)
                stack1.append(top1.right)
                stack2.append(top2.right)
                stack2.append(top2.left)
            else:
                return False
        if not stack1 and not stack2:
            return True
        else:
            return False
```

