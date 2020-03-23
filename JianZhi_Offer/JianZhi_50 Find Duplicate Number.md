# JianZhi- 50 Find Duplicate Number

## Initial Idea
Use hash set.
```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_set<int> S;
        for(auto&num:nums){
            if(S.find(num)!=S.end())
                return num;
            S.insert(num);
        }
        return 0;
    }
}; 
```

## Others' Idea 1
In place swipe, since the length of the array is the same with the range of all numbers. So the array itself is a hash map.
```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        for(int i=0;i<nums.size();++i){
            if(nums[i]!=i){
                if(nums[nums[i]]==nums[i])
                    return nums[i];
                int tmp=nums[nums[i]];
                nums[nums[i]]=nums[i];
                nums[i]=tmp;
            }
        }
        return 0;
    }
}; 
```