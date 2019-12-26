# JianZhi_19 LC_54 - Spiral Matrix

## Initial idea
Print the outside layer in each iteration, but need to handle the corner case when there is only one row or one column left.

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if len(matrix)==0:
            return []
        res=[]
        cL,cR=0,len(matrix[0])-1
        rT,rB=0,len(matrix)-1
        while cL<cR and rT<rB:
            res+=matrix[rT][cL:cR]
            res+=[matrix[i][cR] for i in range(rT,rB)]
            res+=matrix[rB][cR:cL:-1]
            res+=[matrix[i][cL] for i in range(rB,rT,-1)]
            cL+=1
            cR-=1
            rT+=1
            rB-=1
        if rT==rB:
            res+=matrix[rT][cL:cR+1]
        if cL==cR:
            res+=[matrix[i][cR] for i in range(rT,rB+1)]
        if cL==cR and rT==rB: #If there is only one element left, then it will be appended twice in above two 'if' block
            res.pop()
        return res
```

## Or another form of initial idea
In LC 59, this form can avoid handle the corner case when only one element is left. However, here it also can't handle a row or a column corner case, so almost the same with the first one.
```python
class Solution:
    def spiralOrder(self, matrix):
        if len(matrix)==0:
            return []
        res=[]
        cL,cR=0,len(matrix[0])-1
        rT,rB=0,len(matrix)-1
        while cL<cR and rT<rB:
            res+=[matrix[rT][j] for j in range(cL,cR+1)]
            rT+=1
            res+=[matrix[i][cR] for i in range(rT,rB+1)]
            cR-=1
            res+=[matrix[rB][j] for j in range(cR,cL-1,-1)]
            rB-=1
            res+=[matrix[i][cL] for i in range(rB,rT-1,-1)]
            cL+=1
        if cL==cR:
            res+=[matrix[i][cL] for i in range(rT,rB+1)]
        if rT==rB:
            res+=[matrix[rT][j] for j in range(cL,cR+1)]
        if cL==cR and rT==rB:
            res.pop()
        return res
```

## Others' idea 1
We need to print matrix in clock-wise order, so we can get the first row of matrix and then rotate the matrix anti-clockwise. Then the first row in the new matrix is the column we need to get in the previous matrix. Thus, we can do this iteratively until the matrix is empty.

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res=[]
        while matrix:
            res+=matrix.pop(0)
            nextMatrix=[]
            if matrix:
                for j in range(len(matrix[0])-1,-1,-1):
                    nextMatrix.append([matrix[i][j] for i in range(0,len(matrix))])
                matrix=nextMatrix
        return res
```