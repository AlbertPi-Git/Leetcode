# Leetcode 226 - Invert the Binary Tree

## Initial Idea
Bottom to top recursion, time complexity O(N), space complexity O(N).
```c++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==nullptr)
            return root;
        TreeNode* leftNode=invertTree(root->left);
        TreeNode* rightNode=invertTree(root->right);
        root->left=rightNode;
        root->right=leftNode;
        return root;
    }
};
```