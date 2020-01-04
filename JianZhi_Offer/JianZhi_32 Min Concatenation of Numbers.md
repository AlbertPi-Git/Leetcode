# JianZhi_32 - Min Concatenation of Numbers

## Initial idea
Enumerating all permutations, it can be done but complexity is O(N!).

```python
class Solution:
    def __init__(self):
        self.res=None
    def PrintMinNumber(self, numbers):
        def compare(buf,res):
            for i in range(len(buf)):
                if buf[i]<res[i]:
                    return True
                elif buf[i]>res[i]:
                    return False
            return False
        def backtrack(numbers,buf):
            if not numbers:
                if self.res is None:
                    self.res=buf
                else: 
                    if compare(buf,self.res):
                        self.res=buf
                return
            for i in range(len(numbers)):
                backtrack(numbers[:i]+numbers[i+1:],buf+str(numbers[i]))
        backtrack(numbers,'')
        return self.res
```

## Others' idea 1
Start from the original concatenation order, if we swipe two adjacent numbers. The reason why the new concatenation is larger or smaller than the original is the 'value' of local concatenation of that two number changed. So basically it's like a sort problem, but the relationship of two number is not defined by themselves, rather it's defined by the 'value' of their concatenation. e.g. if ab < ba, then a < b. if ab==ba, then a==b, if ab>ba then a>b.

```python
from functools import cmp_to_key
class Solution:
    def PrintMinNumber(self, numbers):
        def comp(left,right):
            if str(left)+str(right)>str(right)+str(left):
                return int(1)
            elif str(left)+str(right)==str(right)+str(left):
                return int(0)
            else:
                return int(-1)
        res=sorted(numbers,key=cmp_to_key(comp))
        res=''.join([str(num) for num in res])
        return res
```