# JianZhi_8 - Jump Stairs

## Initial idea 1
Simple DP
```python
class Solution:
    def jumpFloor(self, number):
        dp=[1]*(number+1)
        for i in range(2,number+1):
            dp[i]=dp[i-1]+dp[i-2]
        return dp[number]
```

## Initial idea 2
Simple recursion, but TLE
```python
class Solution:
    def jumpFloor(self, number):
        if number==0 or number==1:
            return 1
        return self.jumpFloor(number-1)+self.jumpFloor(number-2)
```