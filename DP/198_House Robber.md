# Leetcode 198 - House Robber

## Initial Idea
DP. Differentiate two types of states: withLast[i] holds the max amount can be obtained from first i+1 houses and ith house is included, withoutLast[i] holds the max amount can be obtained when ith house is not included.
```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        else if(nums.size()==1)
            return nums[0];
        else if(nums.size()==2)
            return std::max(nums[0],nums[1]);
        std::vector<int> withLast(nums.size(),0);
        withLast[0]=nums[0];
        withLast[1]=nums[1];
        std::vector<int> withoutLast(nums.size(),0);
        withoutLast[1]=nums[0];
        for(int i=2;i<nums.size();++i){
            withLast[i]=std::max(withoutLast[i-1],std::max(withLast[i-2],withoutLast[i-2]))+nums[i];
            withoutLast[i]=std::max(std::max(withLast[i-1],withoutLast[i-1]),std::max(withLast[i-2],withoutLast[i-2]));
        }
        return std::max(withLast.back(),withoutLast.back());
    }
};
```

## Others' Idea 1
But in fact, there is no need to differentiate whether ith house is included, so no need to use two states.  Let dp[i] holds the max amount can be obtained from first i+1 houses. Then dp[i]=max(dp[i-1],dp[i-2]+nums[i]). 
```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        else if(nums.size()==1)
            return nums[0];
        else if(nums.size()==2)
            return std::max(nums[0],nums[1]);
        std::vector<int> dp(nums.size(),0);
        dp[0]=nums[0];
        dp[1]=std::max(nums[0],nums[1]);
        for(int i=2;i<nums.size();++i){
            dp[i]=std::max(dp[i-1],dp[i-2]+nums[i]);
        }
        return dp.back();
    }
};
```