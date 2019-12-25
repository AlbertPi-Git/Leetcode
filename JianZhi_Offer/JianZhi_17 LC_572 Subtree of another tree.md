# JianZhi_17 LC_572 - Subtree of another tree

## Initial idea 1
Serialize two trees with DFS and generate two strings. If tree2 is the subtree of tree1, then string2 should be the substring of string1. But be careful with two things: 1. if a node is 'None', still need to return ' ' (or any other char except numbers) rather than '', otherwise [2,3] wil be regarded as the subtree of [1,2,3]. 2. need to add a special char (e.g. ',') before each value, otherwise [2] will be regarded as [12].

```python
class Solution:
    def isSubtree(self, root1: TreeNode, root2: TreeNode) -> bool:
        if root2 is None:
            return False
        def PreOrder(root):
            if not root:
                return ' '
            left=PreOrder(root.left)
            right=PreOrder(root.right)
            return ','+str(root.val)+','+left+','+right
        
        serial_1=PreOrder(root1)
        serial_2=PreOrder(root2)
        print(serial_1,serial_2)
        return serial_2 in serial_1
```

## Initial idea 2
Go through the source tree and compare each subtree of the source tree with target tree to see if they are the same. (The code is much messier and slower than the first one)
```python
class Solution:
    def isSubtree(self, root1: TreeNode, root2: TreeNode) -> bool:
        if not root2:
            return False
        def compareTree(root1,root2):
            if (not root1 and root2) or (root1 and not root2):
                return False
            if not root1 and not root2:
                return True
            if root1.val!=root2.val:
                return False
            return compareTree(root1.left,root2.left) and compareTree(root1.right,root2.right)
            
        def Traversal(root):
            if not root:
                return False
            if compareTree(root,root2):
                return True
            return Traversal(root.left) or Traversal(root.right)
        
        return Traversal(root1)
```