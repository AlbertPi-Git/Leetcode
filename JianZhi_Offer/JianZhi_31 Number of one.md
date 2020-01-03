# JianZhi_31 - Number of One

## Initial idea
Traverse every number and count 1 in each number by mod and //10. The time complexity is O(NlogN).

```python
class Solution:
    def NumberOf1Between1AndN_Solution(self, n):
        def OneInNumber(num):
            cnt=0
            while num>0:
                if num%10==1:
                    cnt+=1
                num=num//10
            return cnt
        res=0
        for num in range(1,n+1):
            res+=OneInNumber(num)
        return res
```

## Others' idea
A more mathematic method. Check each digit place of the input number iteratively, i.e. firstly check how many numbers' unit's place is 1 in 1-N? Then ten's place and hundred's place ...

e.g. n=210, for each place, there are three cases: 

1. the digit in that place is 0, e.g. unit's place, then there are 21 numbers whose unit's place is 1. Generally, it's ((n//i)//10)*i (i=1 for unit's place, 10 for ten's place...).  

2. the digit in that place in 1, e.g. ten's place, then there are 21 numbers whose ten's place is 1. Generally, it's ((n//i)//10)*i+(n%i +1).

3. the digit in greater than 1, e.g. hundred's place, then there are 100 numbers whose hundred's place is 1. Generally, it's ((n//i)//10+1)*i.


```python
class Solution:
    def NumberOf1Between1AndN_Solution(self, n):
        res=0
        i=1
        while i<=n:
            quotient=n//i
            remainder=n%i
            if quotient%10==0:
                res+=(quotient//10)*i
            elif quotient%10==1:
                res+=(quotient//10)*i+remainder+1
            else:
                res+=(quotient//10+1)*i
            i*=10
        return res
```