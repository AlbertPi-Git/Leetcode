# JianZhi_7 - Fibonacci

## Initial idea

```python
class Solution:
    def Fibonacci(self, n):
        res=[0,1]+[0]*100
        if n<2:
            return res[n]
        else:
            for i in range(2,n+1):
                res[i]=res[i-1]+res[i-2]
            return res[n]
```