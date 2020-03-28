# JianZhi 60 - Level Order Traversal

## Initial Idea
```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        std::vector<std::vector<int>> res=*new std::vector<std::vector<int>>;
        std::queue<TreeNode*> q;
        if(root)
            q.push(root);
        while(q.size()){
            int len=q.size();
            std::vector<int> tmpRes;
            for(int i=0;i<len;++i){
                TreeNode* tmp=q.front();
                tmpRes.push_back(tmp->val);
                if(tmp->left)
                    q.push(tmp->left);
                if(tmp->right)
                    q.push(tmp->right);
                q.pop();
            }
            if(tmpRes.size())
                res.push_back(tmpRes);
        }
        return res;
    }
};
```