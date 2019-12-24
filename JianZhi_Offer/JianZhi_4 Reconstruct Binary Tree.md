# JianZhi_4 - Reconstruct Binary Tree

## Initial idea
It's easy to identify root node from preOrder list, then it's easy to distinguish left subtree and right subtree with root and inOrder list. Then do the reconstruct recursively.
```python
class Solution:
    def reConstructBinaryTree(self, pre, tin):
        if len(pre)==0:
            return None
        root=TreeNode(pre[0])
        for i in range(len(tin)):
            if tin[i]==pre[0]:
                root.left=self.reConstructBinaryTree(pre[1:i+1],tin[:i])
                root.right=self.reConstructBinaryTree(pre[i+1:],tin[i+1:])
                break
        return root
```