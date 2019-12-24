# JianZhi_9 - Jump Stairs II

## Initial idea 1
Still DP
```python
class Solution:
    def jumpFloorII(self, number):
        dp=[0]*(number+1)
        dp[0],dp[1]=1,1
        for i in range(2,number+1):
            for j in range(i):
                dp[i]+=dp[j]
        return dp[-1]
```
        