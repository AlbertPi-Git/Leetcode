# Leetcode 152 - Max Product Subarray

## Others' Idea 1
DP. Record both max and min product, which is different from 53.
```c++
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int prevMax=nums[0];
        int prevMin=nums[0];
        int res=nums[0];
        for(int i=1;i<nums.size();++i){
            int tmp1=nums[i]*prevMax;
            int tmp2=nums[i]*prevMin;
            prevMax=std::max(nums[i],std::max(tmp1,tmp2));
            prevMin=std::min(nums[i],std::min(tmp1,tmp2));
            res=std::max(res,prevMax);
        }
        return res;
    }
};
```