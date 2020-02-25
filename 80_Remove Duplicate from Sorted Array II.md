# Leetcode 80 - Remove Duplicate from Sorted Array II


```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()<=1)
            return nums.size();
        int slow=0,fast=1;
        int cnt=1;
        for(;fast<nums.size();++fast){
            if(nums[fast]==nums[slow]){
                if(cnt<2){
                    nums[++slow]=nums[fast];
                    ++cnt;
                }
            }else{
                nums[++slow]=nums[fast];
                cnt=1;
            }
        }
        return slow+1;
    }
};
```