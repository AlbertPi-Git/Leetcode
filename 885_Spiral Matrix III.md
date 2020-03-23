# Leetcode 885 - Spiral Matrix III

## Initial idea 1
Simulate the process: left->right, top->bottom, increment distance; right->left, bottom->top, increment distance. Then enter another same iteration until number of points in res is R*C. Note that the point where row and column overlap is appended by the one that is firstly went through. And [r0,c0] is appended before loop to make four inner loop symmetric.
```python
class Solution:
    def spiralMatrixIII(self, R: int, C: int, r0: int, c0: int) -> List[List[int]]:
        res=[[r0,c0]]
        step=1
        r,c=r0,c0
        while len(res)<R*C:
            for j in range(c+1,c+step+1):
                if r>=0 and r<R and j>=0 and j<C:
                    res.append([r,j])
            c=j
            for i in range(r+1,r+step+1):
                if i>=0 and i<R and c>=0 and c<C:
                    res.append([i,c])
            r=i
            step+=1
            for j in range(c-1,c-step-1,-1):
                if r>=0 and r<R and j>=0 and j<C:
                    res.append([r,j])
            c=j
            for i in range(r-1,r-step-1,-1):
                if i>=0 and i<R and c>=0 and c<C:
                    res.append([i,c])
            r=i
            step+=1
        return res
```

