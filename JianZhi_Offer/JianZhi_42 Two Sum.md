# JianZhi 42 - Two Sum

## Initial Idea
Use HashSet to store numbers that already appears. However, in this problem the input is sorted, so two pointers approach is much faster.

```c++
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> nums,int target) {
        int diff=0;
        std::vector<int> res;
        std::unordered_set<int> hashset;
        for(auto &iter:nums){
            if(hashset.find(target-iter)!=hashset.end()&&(2*iter-target>diff)){
                if(res.size()){
                    res.pop_back();
                    res.pop_back();
                }
                res.push_back(target-iter);
                res.push_back(iter);
            }
            hashset.insert(iter);
        }
        return res;
    }
};
```

## Improvement
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::vector<int> res;
        int left=0;
        int right=nums.size()-1;
        while(left<=right){
            if(nums[left]+nums[right]==target){
                res.push_back(nums[left]);
                res.push_back(nums[right]);
                return res;
            }else if(nums[left]+nums[right]<target){
                left++;
            }else{
                right--;
            }
        }
        return res;
    }
};
```