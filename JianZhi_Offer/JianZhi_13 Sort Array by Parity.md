# JianZhi_13 - Sort Array by Parity

## Initial idea
Just go through and use another two additional lists 
```python
class Solution:
    def sortArrayByParity(self, A: List[int]) -> List[int]:
        odd,even=[],[]
        for num in A:
            if num%2:
                odd.append(num)
            else:
                even.append(num)
        return even+odd
```

## In-place operation 1
Use two pointer: front and back, move the pointer towards the center only when the element it points satisfy the condition. (But it can't maintain the original relative order in odd and even part, although in this problem it's not required)
```python
class Solution:
    def sortArrayByParity(self, A: List[int]) -> List[int]:
        even,odd=0,len(A)-1
        while even<odd:
            if A[even]%2==0 and A[odd]%2==1:
                even+=1
                odd-=1
            elif A[even]%2==0 and A[odd]%2==0:
                even+=1
            elif A[even]%2==1 and A[odd]%2==1:
                odd-=1
            else:
                tmp=A[even]
                A[even]=A[odd]
                A[odd]=tmp
        return A
```

## In-place operation 2
To maintain the original relative order, use bubble-sort like operation. However, it increase the time complexity to O(N^2) (Almost forget how to write the most efficient bubble-sort..., decrease the boundary in the direction which bubble goes in each iteration)
```python
class Solution:
    def reOrderArray(self, array):
        for i in range(len(array)-1,-1,-1):
            for j in range(i):
                if array[j]%2==0 and array[j+1]%2==1:
                    tmp=array[j]
                    array[j]=array[j+1]
                    array[j+1]=tmp
        return array
```