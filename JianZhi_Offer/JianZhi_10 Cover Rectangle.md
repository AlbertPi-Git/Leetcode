# JianZhi_9 - Jump Stairs II

## Initial idea 1
Still DP
```python
class Solution:
    def rectCover(self, number):
        dp=[0]*(max(3,number)+1)
        dp[1],dp[2]=1,2
        for i in range(3,number+1):
            dp[i]=dp[i-1]+dp[i-2]
        return dp[number]
```