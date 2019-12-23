# Leetcode 240 - Search a 2D Matrix II

## Initial idea
Since each row of the matrix are sorted, so simply use binary search in each row. Time complexity is O(M*logN).
```python
class Solution:
    def Find(self, target, array):
        if not array or not array[0]:
            return False
        
        def BinSearch(target,lst):
            left,right=0,len(lst)-1
            while left<=right:
                mid=(left+right)//2
                if lst[mid]==target:
                    return True
                elif lst[mid]<target:
                    left=mid+1
                else:
                    right=mid-1
        for lst in array:
            if lst[0]<=target and lst[-1]>=target:
                if BinSearch(target,lst):
                    return True
        return False
```

## Others' idea 1
Value in matrix ascends from left to right and up to bottom, so we can use this order to 'walk' in the matrix. But initial position needs to be chosen carefully. Left-bottom and right-up are two good positions to start since from these position, if target is smaller than current value, just need to move to up/left (left-bottom start/right-up start); while if target is larger than current value, just need to move right/down (left-bottom start/right-up start). So just need to move in two directions, not need to turn back. Time complexity is O(M+N).

```python
class Solution:
    def Find(self, target, array):
        r=len(array)
        c=len(array[0])
        
        i,j=0,c-1
        while i>=0 and i<r and j>=0 and j<c:
            if target==array[i][j]:
                return True
            elif target<array[i][j]:
                j-=1
            else:
                i+=1
        return False
```