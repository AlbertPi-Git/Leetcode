# Leetcode 236 - Lowest Common Ancestor

## Initial Idea
Bottom to top recursion.

```c++
class Solution {
public:
    TreeNode* res;
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        recursion(root,p,q);
        return res;
    }

    int recursion(TreeNode* node,TreeNode* p,TreeNode* q){
        if(node==nullptr)
            return 0;
        int curNode=(node==p||node==q);
        int resL=recursion(node->left,p,q);
        int resR=recursion(node->right,p,q);
        if(resL+resR+curNode==2){
            res=node;
            return 0;
        }else{
            return curNode||resL||resR;
        }
    }
};
```