# Leetcode 53 - Max Sum Subarray

## Initial Idea
Sliding window. But this isn't like the usual sequence sliding window template
```c++
for(move right){
    if(condition is not satisfied)
        move left until condition is satisfied
    compare with current solution to decide whether to replace
}
```
Actually this can be simplified to greedy algorithm below

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res=1<<31;
        int sum=0;
        int left=0;
        for(int right=0;right<nums.size();right++){
            sum+=nums[right];
            res=std::max(sum,res);      //replace is before check the condition, not like usual sliding window template
            if(sum<0){
                //if the beginning of the subarray is positive, then the sum will always be negative, thus,the next condition will always be true. And the beginning of the subarray can't be negative. Thus this while loop is useless and can be removed, which makes this solution the same with greedy one 
                while(left<right&&sum<0){
                    sum-=nums[left];
                    left++;
                }
                if(sum<0){
                    sum=0;
                    left=right+1;
                }
            }
            //res=std::max(sum,res);  //if the replacement is here, it can handle all negative case. (the res will be 0)
        }
        return res;
    }
};
```

## Others' Idea 1
Greedy
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res=1<<31;
        int sum=0;
        for(int right=0;right<nums.size();right++){
            sum+=nums[right];
            res=std::max(sum,res);
            if(sum<0){
                sum=0;
            }
        }
        return res;
    }
};
```

## Others' Idea 2
DP. Let dp[i] be the sum of the subarray that ends at nums[i], the prev=std::max(nums[i],prev+nums[i]) is equal to the sum<0 condition.
```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int prev=nums[0];
        int res=nums[0];
        for(int i=1;i<nums.size();++i){
            prev=std::max(nums[i],prev+nums[i]);
            res=std::max(prev,res);
        }
        return res;
    }
};
```