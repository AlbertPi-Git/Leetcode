# JianZhi 45 - Consecutive in Poker

## Initial Idea
Sort the array firstly, then count the number of 0. Then decrease the count if there is inconsecutive point. If count becomes negative or there is duplicate num, then return false.

```python
class Solution:
    def isStraight(self, nums: List[int]) -> bool:
        nums.sort()
        cnt=int(nums[0]==0)
        for i in range(1,len(nums)):
            if nums[i]==0:
                cnt+=1
            else:
                if nums[i]==nums[i-1]:
                    return False
                if nums[i-1]!=0:
                    cnt-=(nums[i]-nums[i-1]-1)
                if cnt<0:
                    return False
        return True
```

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int cnt=int(nums[0]==0);
        for(int i=1;i<nums.size();i++){
            if(nums[i]==0)
                cnt+=1;
            else{
                if(nums[i]==nums[i-1])
                    return false;
                if(nums[i-1]!=0)
                    cnt-=(nums[i]-nums[i-1]-1);
                if(cnt<0)
                    return false;
            }
        }
        return true;
    }
};
```