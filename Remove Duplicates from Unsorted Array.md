# Remove Duplicates from Unsorted Array

## Initial Idea
Iterate through the array and use hashset to record whether this number has appeared before, if yes then skip, else insert this num to set and assign it to slowIndex+1 (if in-place operation is required, else just append to new array or print it). 

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(!nums.size())
            return 0;
        unordered_set<int> hashset;
        hashset.insert(nums[0]);
        int i=0,j=1;
        for(;j<nums.size();j++){
            if(hashset.find(nums[j])==hashset.end()){
                nums[++i]=nums[j];
                hashset.insert(nums[j]);
            }
        }
        return i+1;
    }
};
```