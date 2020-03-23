# Leetcode 114 - Flatten Binary Tree to Linked List

## Initial Idea
Divide and conquer, divide part is simple, but connecting root,leftSeq,rightSeq part is messy (have to set so many nullptr). 

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        recursion(root);
    }
    //return the tail the flatten sequence
    TreeNode* recursion(TreeNode* root){
        if(root==nullptr)
            return root;
        TreeNode* rightSeqTail=nullptr;
        TreeNode* leftSeqTail=nullptr;
        TreeNode* originalRight=root->right;
        leftSeqTail=recursion(root->left);
        rightSeqTail=recursion(root->right);
        if(leftSeqTail){
            root->right=root->left;
            root->left=nullptr;
            if(originalRight){
                leftSeqTail->right=originalRight;
                rightSeqTail->left=nullptr;
                return rightSeqTail;
            }else{
                leftSeqTail->left=nullptr;
                return leftSeqTail;
            }
        }else{
            if(originalRight){
                rightSeqTail->left=nullptr;
                return rightSeqTail;
            }else{
                return root;
            }     
        }
    }   
};
```

## Others' Idea 1
Iteratively put the path from root's left child to the most right node in the left subtree between root and right subtree.
```c++
class Solution {
public:
    void flatten(TreeNode* root) {  // input root is just a value copy of root pointer, so even we modify the root pointer in function, outside the function it's still the same value, so the tester always accesses the original root.
        while(root!=nullptr){
            if(root->left!=nullptr){
                TreeNode* ptr=root->left;
                while(ptr->right!=nullptr){
                    ptr=ptr->right;
                }
                ptr->right=root->right;
                root->right=root->left;
                root->left=nullptr;
            }
            root=root->right;
        }
    }
};
```