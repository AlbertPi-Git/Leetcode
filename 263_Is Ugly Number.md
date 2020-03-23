# Leetcode 263 - Is Ugly Number

## Initial idea
Keep divide 2 or 3 or 5 until the number doesn't have those factor (this number is not ugly number ) or reach 1 (it is ugly number). 

```python
class Solution:
    def isUgly(self, num: int) -> bool:
        if num<=0:
            return False
        while num>1:
            if num%2==0:
                num/=2
                continue
            if num%3==0:
                num/=3
                continue
            if num%5==0:
                num/=5
                continue
            return False
        return True
```