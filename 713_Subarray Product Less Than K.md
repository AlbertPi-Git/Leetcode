# Leetcode 713 - Subarray Product Less Than K

## Others' idea 1
Sliding window

```c++
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        int left,right,res;
        left=right=res=0;
        int Mul=1;
        for(;right<nums.size();right++){
            Mul*=nums[right];
            while(Mul>=k && left<=right){
                Mul/=nums[left];
                left++;
            }
            if(left<=right){
                res+=right-left+1;
            }
        }
        return res;
    }
};
```

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        left,right=0,0
        Mul=1
        res=0
        for right in range(len(nums)):
            Mul*=nums[right]
            while Mul>=k and left<=right:
                Mul/=nums[left]
                left+=1
            if Mul<k:
                res+=right-left+1
        return res
```