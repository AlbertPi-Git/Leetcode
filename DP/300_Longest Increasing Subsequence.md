# Leetcode 300 - Longest Increasing Subsequence

## Initial Idea
DP. Since this is a subsequence problem, so the chosen elements are not consecutive, so the current state depends on all states before it. The time complexity is O(N^2). dp[i] holds the length of the LIS that ends at nums[i].
```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.empty())
            return 0;
        std::vector<int> dp=std::vector<int>(nums.size(),1);
        for(int i=1;i<nums.size();++i){
            for(int j=0;j<i;++j){
                if(nums[j]<nums[i])
                    dp[i]=std::max(dp[j]+1,dp[i]);
            }
        }
        return *std::max_element(dp.begin(),dp.end());
    }
};
```

## Others' Idea 1
In first method, for each dp[i] we need to iterate through all previous dp elements to find the suitable longest subsequence, which is inefficient. In fact, we can let dp[i] holds the last elements of the subsequence whose length is i. To obtain the longest subsequence, we should keep the last element as small as possible. So when we iterate through nums, we use binary search to find the longest subsequence whose last element is smaller than nums[i], and append nums[i] to that sequence to form a new sequence.
```c++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.empty())
            return 0;
        std::vector<int> dp=std::vector<int>(nums.size(),INT_MAX);
        dp[0]=nums[0];
        int curMax=1;
        for(int i=1;i<nums.size();++i){
            //lower_bound will return the iterator of the first element which is greater or equal to nums[i]
            auto lb=std::lower_bound(dp.begin(),dp.begin()+curMax,nums[i]);
            // e.g. find 7 in [6,8], then lb will point to 8. We actually append 7 the 6's subsequence, but then the new sequence will has the same length with 8's sequence and 7 is smaller than 8, so we will replace 8 with 7.
            //if it's [6,7,8], we just replace 7 with 7, so nothing happens
            *lb=nums[i];
            if(lb-dp.begin()==curMax)   // if nums[i] is appended to the current longest subsequence, then we need to increment curMax
                ++curMax;
        }
        return curMax;
    }
};
```