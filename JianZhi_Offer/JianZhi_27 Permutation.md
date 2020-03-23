# JianZhi_27 - Permutation

## Initial idea
```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res=[]
        nums.sort()
        def backtrack(s,buf):
            if not s and buf:
                res.append(buf)
            for i in range(len(s)):
                if i>0 and s[i]==s[i-1]:   
                    continue                 
                backtrack(s[:i]+s[i+1:],buf+[s[i]])
        backtrack(nums,[])
        return res
```
