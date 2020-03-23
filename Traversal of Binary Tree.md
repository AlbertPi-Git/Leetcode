# Leetcode 144, 94, 145, 102 - PreOrder, InOrder, PostOrder and LevelOrder Traversal of Binary Tree

## PreOrder Traversal
### Recursively
Recursive traversal is trivial.
```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res=[]
        def preOrder(root):
            if not root:
                return
            res.append(root.val)
            preOrder(root.left)
            preOrder(root.right)
        preOrder(root)
        return res
```

### Iteratively 1
This is my initial iterative implementation, use the stack to hold both left and right child of root. But this method doesn't compatible with InOrder and PreOrder, so better to remember the second method.
```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res=[]
        stack=[root] if root else []
        while stack:
            top=stack.pop()
            res.append(top.val)
            if top.right:
                stack.append(top.right)
            if top.left:
                stack.append(top.left)
        return res
```

### Iteratively 2
Use cur pointer to point current node, only use the stack to hold the right child before set cur to current left child so that when it comes back, it knows the next node.
```python
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res,stack=[],[]
        cur=root
        while cur or stack:
            if cur:
                res.append(cur.val)
                if cur.right:
                    stack.append(cur.right)
                cur=cur.left
            else:
                cur=stack.pop()
        return res
```

## InOrder Traversal
### Recursively
Recursive traversal is trivial.
```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res=[]
        def inOrder(root):
            if not root:
                return
            inOrder(root.left)
            res.append(root.val)
            inOrder(root.right)
        inOrder(root)
        return res
```

### Iteratively
As compared with PreOrder, the stack here hold root rather than right, since after comes back from left child, it then appends root.val. What's more, right child is also known once the root is obtained.
```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res,stack=[],[]
        cur=root
        while cur or stack:
            if cur:
                stack.append(cur)
                cur=cur.left
            else:
                top=stack.pop()
                res.append(top.val)
                cur=top.right        
        return res
``` 

## PostOrder Traversal
### Recursively
Recursive traversal is trivial.
```python
class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        res=[]
        def PostOrder(root):
            if not root:
                return
            PostOrder(root.left)
            PostOrder(root.right)
            res.append(root.val)
        PostOrder(root)
        return res
```

### Iteratively 1
PostOrder require both current node and right child to be hold in the stack, but when popped out from stack, operations on root and right are different. Append to res when it's root, keep searching when it's right. So use a mark to differentiate root and right child.
```python
class Solution:
    def postorderTraversal(self, root: TreeNode):
        res,stack=[],[]
        cur=root
        while cur or stack:
            if cur:
                stack.append(('root',cur))
                if cur.right:
                    stack.append(('right',cur.right))
                cur=cur.left
            else:
                top=stack.pop()
                if top[0]=='root':
                    res.append(top[1].val)
                else:
                    cur=top[1]
        return res
``` 

### Iteratively 2
Only need to do the root-right-left 'InOrder-like' traversal and then reverse the res, which can naturally generate left-right-root order.  But this only applies to print value of each node, if it's a series of operations on each node that require to be done in strict PostOrder, then this method has to generate the res list and then do the operations. While the previous iterative method can do that in once.  
```python
class Solution:
    def postorderTraversal(self, root: TreeNode):
        res,stack=[],[]
        cur=root
        while cur or stack:
            if cur:
                res.append(cur.val)
                if cur.left:
                    stack.append(cur.left)
                cur=cur.right
            else:
                cur=stack.pop()
        return res[::-1]
```

## LevelOrder Traversal
### Iteratively
Not the most easy type of levelOrder traversal, since need to put different layer in different list, but can still use queue to solve easily.
```python
from collections import deque
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        res=[]
        Q=deque([[root]]) if root else deque()
        while Q:
            frontLevel=Q.popleft()
            res.append([node.val for node in frontLevel])
            nextLevel=[]
            for node in frontLevel:
                if node.left:
                    nextLevel.append(node.left)
                if node.right:
                    nextLevel.append(node.right)
            if nextLevel:
                Q.append(nextLevel)
        return res
```
