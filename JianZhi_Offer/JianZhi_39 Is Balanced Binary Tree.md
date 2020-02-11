# JianZhi 39 - Is Balanced Binary Tree

## Initial Idea
Recursively check whether each node's left and right tree satisfy the balanced condition.

python
```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        
        def treeHeight(node):
            if not node:
                return 0
            leftHeight=treeHeight(node.left)
            if leftHeight<0:
                return -1
            rightHeight=treeHeight(node.right)
            if rightHeight<0:
                return -1
            
            return max(leftHeight,rightHeight)+1 if abs(leftHeight-rightHeight)<=1 else -1
        
        height=treeHeight(root)
        return height>=0
```

C++
```c++
class Solution {
public:
    int height(TreeNode* node){
        if(node==nullptr)
            return 0;
        int heightL=height(node->left);
        if(heightL<0)
            return -1;
        int heightR=height(node->right);
        if(heightR<0)
            return -1;
        if(std::abs(heightL-heightR)<=1)
            return std::max(heightL,heightR)+1;
        else
            return -1;
    }
    bool isBalanced(TreeNode* root) {
        int heightRoot=height(root);
        return heightRoot>=0;
    }
};
```