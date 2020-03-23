# Leetcode 26 - Remove Duplicate from Sorted Array

https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/

## Others' Idea 1
Use slow and fast pointer. Slow pointer satisfies that subarray on the left of the slow pointer (include slow pointer position) doesn't contain duplicate. Make fast pointer iterates through the array, if a[ fast]==a[ slow] then just continue since they are the duplicate of the value slow pointer points to, if a[ fast]!=a[ slow], then assign a[ j] to a[ i+1], then i++, j++.

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        int i=0,j=1;
        while(j<nums.size()){
            if(nums[i]!=nums[j])
                nums[++i]=nums[j];
            ++j;
        }
        return i+1;
    }
};
```

