# JianZhi 58 - Is Binary Tree Symmetric

## Initial Idea
Do two in-order traversal (cur->left->right) and (cur->right->left) and store the elements in two vectors, then compare whether two vectors are the same.
```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        std::vector<int> resL;
        std::vector<int> resR;
        std::vector<TreeNode*> stack;
        stack.push_back(root);
        while(stack.size()){
            TreeNode* tmp=stack.back();
            stack.pop_back();
            if(tmp){
                resL.push_back(tmp->val);
                stack.push_back(tmp->left);
                stack.push_back(tmp->right);
            }else{
                resL.push_back(-1);
            } 
        }
        stack.push_back(root);
        while(stack.size()){
            TreeNode* tmp=stack.back();
            stack.pop_back();
            if(tmp){
                resR.push_back(tmp->val);
                stack.push_back(tmp->right);
                stack.push_back(tmp->left);
            }else{
                resR.push_back(-1);
            }
        }
        return resL==resR;
    }
};
```

## Idea 2
Do level traversal.
```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        std::queue<TreeNode*> q;
        std::vector<int> resL;
        std::vector<int> resR;
        q.push(root);
        while(q.size()){
            TreeNode* tmp=q.front();
            q.pop();
            if(tmp){
                resL.push_back(tmp->val);
                q.push(tmp->left);
                q.push(tmp->right);
            }else{
                resL.push_back(-1);
            }
        }
        q.push(root);
        while(q.size()){
            TreeNode* tmp=q.front();
            q.pop();
            if(tmp){
                resR.push_back(tmp->val);
                q.push(tmp->right);
                q.push(tmp->left);
            }else{
                resR.push_back(-1);
            }
        }
        return resL==resR;
    }
};
```

## Others' Idea 1
recursion
```c++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        return recurCheck(root->left,root->right);
    }

    bool recurCheck(TreeNode* left,TreeNode* right){
        if(!left && !right)
            return true;
        if(!(left&&right))
            return false;
        if(left->val!=right->val)
            return false;
        return recurCheck(left->left,right->right) && recurCheck(left->right,right->left);
    }
};
```

