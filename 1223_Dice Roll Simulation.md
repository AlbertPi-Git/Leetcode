# Leetcode 1223 - Dice Roll Simulation

## Others' Idea 1
3 dimension DP, dp[i][j][k] means number of unique sequences in first i rolls that end with number j and j appears k consecutive times at that point. (Actually it can be reduced to 2 dimension DP since dp[i][...][...] only relate with dp[i][...][...] and dp[i-1][...][...])

```python
class Solution:
    def dieSimulator(self, n: int, rollMax: List[int]) -> int:
        rollMax=[0]+rollMax
        dp=[[[0]*(max(rollMax)+1) for _ in range(7)] for _ in range(n)]
        for j in range(1,7):
                dp[0][j][1]=1
        for i in range(1,n):
            for j in range(1,7):
                for k in range(1,rollMax[j]+1):
                    if k==1:
                        Sum=0
                        for m in range(1,7):
                            if m!=j:
                                for l in range(1,rollMax[m]+1):
                                    Sum+=dp[i-1][m][l]
                        dp[i][j][k]=Sum
                    else:
                        dp[i][j][k]=dp[i-1][j][k-1]
        res=0
        for j in range(1,7):
            for k in range(1,rollMax[j]+1):
                res+=dp[n-1][j][k]
        return res%(10**9+7)
```