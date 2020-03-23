# JianZhi 57 - Next TreeNode in In-order traversal order

## Initial Idea (and others' idea)
```c++
class Solution {
public:
    TreeLinkNode* GetNext(TreeLinkNode* pNode)
    {
        std::vector<TreeLinkNode*> stack;
        TreeLinkNode* res=nullptr;
        if(pNode->right||pNode->next==nullptr){
            if(pNode->right)
                stack.push_back(pNode->right);
            while(stack.size()){
                res=stack.back();
                stack.pop_back();
                if(res->left)
                    stack.push_back(res->left);
            }
            return res;
        }else{
            if(pNode->next->left==pNode)
                return pNode->next;
            else{
                res=pNode;
                while(res->next!=nullptr&&res->next->right==res)
                    res=res->next;
                return res->next;
            }
        }
    }
};
```

## A shorter one
```c++
class Solution {
public:
    TreeLinkNode* GetNext(TreeLinkNode* pNode)
    {
        if(pNode==nullptr)
            return nullptr;
        if(pNode->right){
            pNode=pNode->right;
            while(pNode->left)
                pNode=pNode->left;
            return pNode;
        }else if(pNode->next==nullptr){
            return nullptr;
        }else{
            if(pNode->next->left==pNode)
                return pNode->next;
            else{
                while(pNode->next!=nullptr&&pNode->next->right==pNode)
                    pNode=pNode->next;
                return pNode->next;
            }
        }
    }
};
```