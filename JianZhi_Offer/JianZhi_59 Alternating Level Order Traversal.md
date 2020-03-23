# JianZhi 59 - Alternating Level Order Traversal

## Initial Idea
Use a vector to contain the all nodes in a layer, then put this vector into queue to do level order traversal. The put order of vector if always from left to right, while the getting value order is different in even and odd layer.
```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        std::vector<std::vector<int>> res=*new std::vector<std::vector<int>>;
        if(!root)
            return res;
        std::queue<std::vector<TreeNode*>> q;
        std::vector<TreeNode*> levelVec;
        levelVec.push_back(root);
        int depth=1;
        q.push(levelVec);
        while(q.size()){
            std::vector<TreeNode*> tmp=q.front();
            q.pop();
            std::vector<int> tmpRes;
            std::vector<TreeNode*> next;
            if(depth%2==1){
                for(int i=0;i<tmp.size();++i){
                    tmpRes.push_back(tmp[i]->val);
                }
            }else{
                for(int i=tmp.size()-1;i>=0;--i){
                    tmpRes.push_back(tmp[i]->val);
                }
            }
            for(auto& node: tmp){
                if(node->left)
                    next.push_back(node->left);
                if(node->right)
                    next.push_back(node->right);
            }
            res.push_back(tmpRes);
            if(next.size())
                q.push(next);
            depth++;
        }
        return res;
    }
};
```

## Others' Idea 1
No need to do put all nodes in a layer into a vector, just record the size of the queue at the beginning of the loop, then we know which elements belongs to this layer and which elements belongs to next layer.
```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        std::vector<std::vector<int>> res=*new std::vector<std::vector<int>>;
        if(!root)
            return res;
        std::queue<TreeNode*> q;
        q.push(root);
        int depth=1;
        while(q.size()){
            int len=q.size();
            std::vector<int> tmpRes;
            for(int i=0;i<len;++i){
                TreeNode* tmpNode=q.front();
                q.pop();
                tmpRes.push_back(tmpNode->val);
                if(tmpNode->left)
                    q.push(tmpNode->left);
                if(tmpNode->right)
                    q.push(tmpNode->right);
            }
            if(depth%2==0)
                std::reverse(tmpRes.begin(),tmpRes.end());
            res.push_back(tmpRes);
            depth++;
        }
        return res;
    }
};
```