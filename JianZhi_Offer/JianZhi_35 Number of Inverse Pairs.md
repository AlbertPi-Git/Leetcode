# JianZhi_35 - Number of Inverse Pairs

## Initial idea
Brutal force compare, but time complexity O(N^2) is too high.

## Others' idea
How many inverse pairs in list==how many swipes needs to be taken to change this list to an ascending sorted list. So basically we can use divide and merge sort so that time complexity is O(NlogN). Additionally, we need to count number of swipes during the sort.  
```python
class Solution:
    def __init__(self):
        self.cnt=0
    def InversePairs(self, nums):
        def merge(left,right):
            res=[]
            indexL,indexR=0,0
            lenL,lenR=len(left),len(right)
            while indexL<lenL and indexR<lenR:
                if left[indexL]<right[indexR]:
                    res.append(left[indexL])
                    indexL+=1
                else:
                    res.append(right[indexR])
                    indexR+=1
                    self.cnt+=(lenL-indexL)
            if indexL<lenL:
                res+=left[indexL:]
            else:
                res+=right[indexR:]
            return res
                
        def divide(nums):
            if len(nums)==1:
                return nums
            mid=len(nums)//2
            left=divide(nums[:mid])
            right=divide(nums[mid:])
            res=merge(left,right)
            return res
        divide(nums)
        return self.cnt%1000000007
```

Another implementation (try to make it faster but still, it can only pass 75% test cases)
```python
class Solution:
    def __init__(self):
        self.cnt=0
    def InversePairs(self, nums):
        def merge(posL,mid,posR):
            res=[0]*(posR-posL+1)
            resIndex=0
            indexL,indexR=posL,mid
            while indexL<mid and indexR<posR+1:
                if nums[indexL]<nums[indexR]:
                    res[resIndex]=nums[indexL]
                    resIndex+=1
                    indexL+=1
                else:
                    res[resIndex]=nums[indexR]
                    resIndex+=1
                    indexR+=1
                    self.cnt+=(mid-indexL)
            if indexL<mid:
                for i in range(indexL,mid):
                    res[resIndex]=nums[i]
                    resIndex+=1
            else:
                for i in range(indexR,posR+1):
                    res[resIndex]=nums[i]
                    resIndex+=1
            for i in range(posL,posR+1):
                nums[i]=res[i-posL]
                
        def divide(posL,posR):
            if posL==posR:
                return
            mid=(posL+posR+1)//2
            divide(posL,mid-1)
            divide(mid,posR)
            merge(posL,mid,posR)
            return
        divide(0,len(nums)-1)
        return self.cnt%1000000007
```