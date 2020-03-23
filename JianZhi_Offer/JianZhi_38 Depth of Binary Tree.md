# JianZhi 38 - Depth of Binary Tree

## Initial Idea
DFS

python, iterative
```python
class Solution:
    def TreeDepth(self, pRoot):
        # write code here
        if not pRoot:
            return 0
        stack=[(pRoot,1)]
        res=0
        while stack:
            top,depth=stack.pop()
            if top.right:
                stack.append((top.right,depth+1))
            if top.left:
                stack.append((top.left,depth+1))
            if not top.left and not top.right:
                res=max(res,depth)
        return res
```

python, recursive
```python
class Solution:
    def __init__(self):
        self.res=0
    def TreeDepth(self, pRoot):
        # write code here
        if not pRoot:
            return 0
        
        def recursion(node,depth):
            if not node:
                self.res=max(self.res,depth-1)
                return
            recursion(node.left,depth+1)
            recursion(node.right,depth+1)
        recursion(pRoot,1)
        return self.res
```

C++, iterative
```c++
#include<vector>
class Solution {
public:
    int TreeDepth(TreeNode* pRoot)
    {
        if(pRoot==nullptr)
            return 0;
        typedef std::pair<TreeNode*,int> stackNode;
        std::vector<stackNode> stack;
        stack.push_back(std::make_pair(pRoot,1));
        int res=0;
        while(stack.size()){
            stackNode top=stack.back();
            stack.pop_back();
            if(top.first->right!=nullptr)
                stack.push_back(std::make_pair(top.first->right,top.second+1));
            if(top.first->left!=nullptr)
                stack.push_back(std::make_pair(top.first->left,top.second+1));
            if(top.first->left==nullptr&&top.first->right==nullptr)
                res=std::max(res,top.second);
        }
            return res;
    }
};
```

C++, recursive
```c++
class Solution {
public:
    int res=0;
    void recursion(TreeNode* node,int depth){
        if(node==nullptr){
            res=std::max(res,depth-1);
            return;
        }
        recursion(node->left,depth+1);
        recursion(node->right,depth+1);
    }
    
    int TreeDepth(TreeNode* pRoot)
    {
        if(pRoot==nullptr)
            return 0;
        recursion(pRoot,1);
        return res;
    }
};
```