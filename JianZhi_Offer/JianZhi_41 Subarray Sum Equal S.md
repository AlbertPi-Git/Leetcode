# JianZhi 41 Leetcode 829 - Subarray Sum Equal S

## Initial Idea
Sliding window, while the time complexity is O(N), so TLE in LC829.
```python
class Solution:
    def FindContinuousSequence(self, tsum):
        Sum=0
        left=1
        res=[]
        for right in range(1,(tsum//2)+2):
            Sum+=right
            if Sum>tsum:
                while Sum>tsum and left<right:
                    Sum-=left
                    left+=1
            if Sum==tsum and right>left:
                res.append([i for i in range(left,right+1)])
        return res
```

## Others' Idea 1
https://leetcode-cn.com/problems/consecutive-numbers-sum/solution/pythonchao-hao-li-jie-de-onsuan-fa-by-yybeta/
len(sequence) is 1: x==N <=> (N-0)%1==0
len(sequence) is 2: x+x+1==N <=> (N-0-1)%2==0
...
len(sequence) is k: x+1+...x+k==N <=>(N-0-1-...-(k-1))%k==0

```python
class Solution:
    def consecutiveNumbersSum(self, N: int) -> int:
        res, i = 0, 1
        while N > 0:
            res += N % i == 0
            N -= i
            i += 1
        return res
```
