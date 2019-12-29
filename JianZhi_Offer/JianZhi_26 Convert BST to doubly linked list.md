# JianZhi_26 - Convert BST to doubly linked list

## Initial idea
In-order traverse BST and put the result into res list, then construct doubly linked list from res.

Recursive version
```python
class Solution:
    def Convert(self, root):
        if not root:
            return None
        res=[]
        def dfs(root):
            if not root:
                return
            dfs(root.left)
            res.append(root)
            dfs(root.right)
        dfs(root)
        dummy=TreeNode(None)
        prev=dummy
        for node in res:
            node.left=prev
            prev.right=node
            prev=node
        res=dummy.right
        res.left=None
        return res
```

Iterative version
```python
class Solution:
    def Convert(self, root):
        if not root:
            return None
        res=[]
        stack=[]
        cur=root
        while cur or stack:
            if cur:
                stack.append(cur)
                cur=cur.left
            else:
                cur=stack.pop()
                res.append(cur)
                cur=cur.right
        dummy=TreeNode(None)
        prev=dummy
        for node in res:
            node.left=prev
            prev.right=node
            prev=node
        res=dummy.right
        res.left=None
        return res
```

## Others' idea 1
More directly, start the convert inside the recursion function. The recursion function returns the head and tail of the converted doubly linked list.
```python
class Solution:
    def Convert(self, root):
        if not root:
            return None
        def Serialize(root):
            if not root.left and not root.right:
                return (root,root)
            if root.left and root.right:
                head,tail_left=Serialize(root.left)
                tail_left.right=root
                root.left=tail_left
                head_right,tail=Serialize(root.right)
                head_right.left=root
                root.right=head_right
            elif root.left:
                head,tail_left=Serialize(root.left)
                tail_left.right=root
                root.left=tail_left
                tail=root
            else:
                head_right,tail=Serialize(root.right)
                head_right.left=root
                root.right=head_right
                head=root
            head.left=None
            tail.right=None
            return head,tail
        res,_=Serialize(root)
        return res
``` 