# Leetcode 56 - Merge Interval

## Initial Idea (Part of others' idea)
Sort all intervals based on their start position, so that all intervals that can be merged must be adjacent.
```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        std::sort(intervals.begin(),intervals.end());
        std::vector<std::vector<int>> res=*new std::vector<std::vector<int>>;
        for(auto&inter:intervals){
            if(res.size()==0){
                res.push_back(inter);
            }else{
                auto&last=res.back();
                if(inter[0]<=last[1])
                    last[1]=max(last[1],inter[1]);
                else
                    res.push_back(inter);
            }
        }
        return res;
    }
};
```