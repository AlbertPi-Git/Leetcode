# Leetcode 1177 - Can Make Palindrome from Substring

## Initial Idea
Count each char in the substring and take care of those appear odd number of times, if number of chars that appear odd number of times - k is smaller than length of substring%2 then we can make the substring a palindrome. k>=13 constraint comes from the fact that: there are at most 26 chars that appear odd number of times so as long as k>=13, it's guaranteed that this substring can be made a palindrome. 

```python
from collections import Counter
class Solution:
    def canMakePaliQueries(self, s: str, queries: List[List[int]]) -> List[bool]:
        res=[]
        for left,right,k in queries:
            if k>=13:
                res.append(True)
                continue
            substr=s[left:right+1]
            cnt=0
            hashmap=Counter(substr)
            for key in hashmap:
                if hashmap[key]%2==1:
                    cnt+=1
            if cnt-k*2<=(right-left+1)%2:
                res.append(True)
            else:
                res.append(False)
        return res
```