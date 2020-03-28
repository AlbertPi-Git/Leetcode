# Leetcode 674 - Longest Increasing Subarray

## Initial Idea
DP.(Greedy is the same with DP in this problem)
```c++
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        if(nums.empty())
            return 0;
        int res=1;
        int cnt=1;
        for(int i=1;i<nums.size();++i){
            if(nums[i]>nums[i-1])
                ++cnt;
            else
                cnt=1;
            res=std::max(res,cnt);
        }
        return res;
    }
};
```