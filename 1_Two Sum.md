# Leetcode 1 - Two Sum

## Initial Idea
HashMap
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::unordered_map<int,int> hashMap;
        for(int i=0;i<nums.size();++i){
            if(hashMap.find(target-nums[i])!=hashMap.end()){
                return {hashMap[target-nums[i]],i};
            }else{
                hashMap[nums[i]]=i;
            }
        }
        return {};
    }
};
```

## Follow up
If the array is sorted, then we can use two pointer search from begin and end, so that space complexity can be reduced to O(1).