# Leetcode 59 - Spiral Matrix II

## Initial idea 1
Fill the outside layer in each iteration. A little bit different from LC 54, since matrix is always a square, so no need to consider one row or one column left case.
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix=[[0]*n for _ in range(n)]
        rT,rB=0,n-1
        cL,cR=0,n-1
        cur=1
        while cL<cR and rT<rB:
            for j in range(cL,cR):
                matrix[rT][j]=cur
                cur+=1
            for i in range(rT,rB):
                matrix[i][cR]=cur
                cur+=1
            for j in range(cR,cL,-1):
                matrix[rB][j]=cur
                cur+=1
            for i in range(rB,rT,-1):
                matrix[i][cL]=cur
                cur+=1
            rT+=1
            rB-=1
            cL+=1
            cR-=1
        if rT==rB and cL==cR: 
            matrix[rT][cL]=cur
        return matrix
```

## Improvement
Modify four boundaries after writing a row or column is done, so that no need to separately consider rT==rB and cL==cR this corner case.
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix=[[0]*n for _ in range(n)]
        rT,rB=0,n-1
        cL,cR=0,n-1
        cur=1
        while cur<=n**2:
            for j in range(cL,cR+1):
                matrix[rT][j]=cur
                cur+=1
            rT+=1
            for i in range(rT,rB+1):
                matrix[i][cR]=cur
                cur+=1
            cR-=1
            for j in range(cR,cL-1,-1):
                matrix[rB][j]=cur
                cur+=1
            rB-=1
            for i in range(rB,rT-1,-1):
                matrix[i][cL]=cur
                cur+=1
            cL+=1
        return matrix
```

