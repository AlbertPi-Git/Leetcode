# Leetcode 189 - Rotate Array

## Initial Idea 1
Naively right rotate k times, but TLE.

## Initial Idea 2
Use tmp array whose size is k, technically k is not related with n, so can be regarded as O(1)? But the worst case is still O(N).
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        k=k%nums.size();
        std::vector<int> tmp(k,0);
        for(int i=nums.size()-k;i<nums.size();++i)
            tmp[i-nums.size()+k]=nums[i];
        for(int i=nums.size()-1;i>=k;--i)
            nums[i]=nums[i-k];
        for(int i=0;i<k;++i)
            nums[i]=tmp[i];
    }
};
```

## Others' Idea 1
Reverse three times, strictly O(1).
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int len=nums.size();
        k=k%len;
        reverse(nums,0,len-1);
        reverse(nums,0,k-1);
        reverse(nums,k,len-1);
    }
    
    void reverse(vector<int>& nums,int begin,int end){
        int i=begin;
        int j=end;
        while(i<j){
            std::swap(nums[i],nums[j]);
            ++i;
            --j;
        }
    }
};
```

