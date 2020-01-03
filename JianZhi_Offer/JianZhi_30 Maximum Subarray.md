# JianZhi_30 LC 53 - Maximum Subarray

## Initial idea
Thought of sliding window firstly, but this one doesn't need that. Because if a subarray doesn't satisfy the requirement, we will start directly from current number, so no moving left process. If curSum<0 then add current number to it, else set curSum as current number.

```python
class Solution:
    def maxSubArray(self, array):
        res=-2**32
        curSum=-2**32
        for num in array:
            if curSum<0:
                curSum=num
            else:
                curSum+=num
            res=max(res,curSum)
        return res
```