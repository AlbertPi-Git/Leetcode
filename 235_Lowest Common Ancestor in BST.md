# Leetcode 235 - Lowest Common Ancestor in BST

## Initial Idea
Deal with it like the 236 Lowest Common Ancestor in normal binary tree

## Others' Idea 1
BST is ordered, so we can know which subtree (left or right) are p and q on. If they are not on the same subtree (including the cases: 1. p or q is the node 2. p and q are on different subtree), then current node is the LCA, else keep cursively searching that subtree. 

```c++
class Solution {
public:
    TreeNode* res;
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        recursion(root,p,q);
        return res;
    }

    void recursion(TreeNode* node,TreeNode* p,TreeNode* q){
        if(p->val>node->val&&q->val>node->val)
            recursion(node->right,p,q);
        else if(p->val<node->val&&q->val<node->val)
            recursion(node->left,p,q);
        else
            res=node;
    }
};
```

## Others' Idea 2
Since if p,q are not on the same subtree, current node is LCA, so there is only one unique path to search, which means we can just use loop to do this.

```c++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        int Pval=p->val, Qval=q->val;
        TreeNode* node=root;
        while(node!=nullptr){
            if(Pval>node->val&&Qval>node->val){
                node=node->right;
            }else if(Pval<node->val&&Qval<node->val){
                node=node->left;
            }else{
                return node;
            }
        }
        return node;
    }
};
```