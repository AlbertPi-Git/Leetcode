# Leetcode 149 - Max Points on a Line

## Others' Idea 1
We have to check the line formed by any two points at least once, so the time complexity is at least O(N^2). For each point, use hashmap to store slope rates of lines that it resides and number of other points that are on the same line. Find max for this point and compare with current global max. We only need to check other points that are behind current one in the array since pairs with previous ones have been considered before.

```python
from collections import Counter
class Solution:
    def maxPoints(self, points: List[List[int]]) -> int:
        
        def K(i,j):
            return float('Inf') if i[1] - j[1] == 0 else (i[0] - j[0]) / (i[1] - j[1]) 

        if len(points) <= 2:
            return len(points)
        
        res = 0
        for i in range(len(points)):
            same=sum([1 for j in range(i,len(points)) if points[j]==points[i]])
            hashmap=Counter([K(points[i],points[j]) for j in range(i+1,len(points)) if points[i]!=points[j]])
            tmpmax=hashmap.most_common(1)[0][1] if hashmap else 0
            res=max(same+tmpmax,res)
        
        return res
```