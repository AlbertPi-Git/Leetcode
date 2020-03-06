# Leetcode 114 - Flatten Binary Tree to Linked List

## Initial Idea
Divide and conquer, divide part is simple, but connecting root,leftSeq,rightSeq part is messy (have to set so many nullptr). 

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        recursion(root);
    }
    //return tail the flatten sequence
    TreeNode* recursion(TreeNode* root){
        if(root==nullptr)
            return root;
        TreeNode* rightSeqTail=nullptr;
        TreeNode* leftSeqTail=nullptr;
        TreeNode* originalRight=root->right;
        if(root->left)
            leftSeqTail=recursion(root->left);
        if(originalRight)
            rightSeqTail=recursion(root->right);
        if(root->left){
            root->right=root->left;
            root->left=nullptr;
            if(originalRight){
                leftSeqTail->right=originalRight;
                rightSeqTail->left=nullptr;
                rightSeqTail->right=nullptr;
                return rightSeqTail;
            }else{
                leftSeqTail->left=nullptr;
                leftSeqTail->right=nullptr;
                return leftSeqTail;
            }
        }else{
            if(originalRight){
                rightSeqTail->left=nullptr;
                rightSeqTail->right=nullptr;
                return rightSeqTail;
            }else{
                return root;
            }     
        }
    }   
};
```