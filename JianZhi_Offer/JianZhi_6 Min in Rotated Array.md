# JianZhi_6 - Min in Rotated Array

## Initial idea
It's similar with finding target value in a rotated array, however, since we don't know the min value in advance, so we won't know current value is the min value. So each time we compare with current result and set the min of them as new result. 
```python
class Solution:
    def minNumberInRotateArray(self, rotateArray):
        if len(rotateArray)==0:
            return 0
        left,right=0,len(rotateArray)-1
        res=999999999999999
        while left<=right:
            mid=(left+right)//2
            res=min(res,rotateArray[mid])
            if rotateArray[mid]>rotateArray[right]:
                left=mid+1
            else:
                right=mid-1
        return res
```