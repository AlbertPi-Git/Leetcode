# JianZhi_29 - Least K numbers

## Initial idea
Do incomplete bubble sort, so that K numbers in the front of the list are sorted. Time complexity is O(N*K). Almost forget bubble sort again... The iteration direction of outer loop and inner loop are opposite. 
```python
class Solution:
    def GetLeastNumbers_Solution(self, numbers, k):
        if k>len(numbers):
            return []
        for i in range(k):
            for j in range(len(numbers)-1,i,-1):
                if numbers[j]<numbers[j-1]:
                    tmp=numbers[j]
                    numbers[j]=numbers[j-1]
                    numbers[j-1]=tmp
        return numbers[:k]
```

## Others' idea
Since we only need to find the least K numbers, those comparisons between left N-K numbers are redundant. We can set up a heap and maintain numbers in it less or equal to K. Go through the list and then numbers in the heap are the results.

### Use heap in python
Python only provides min heap, but we need max heap here because we need to remove max value in heap when it's full and we want to add new number to it. So we add number to heap and pop number from heap to res, we times -1 to make use of this min heap.
```python
import heapq
class Solution:
    def GetLeastNumbers_Solution(self, numbers, k):
        if k>len(numbers) or k==0:
            return []
        heap=[]
        for num in numbers:
            if len(heap)<k:
                heapq.heappush(heap,-1*num)
            else:
                heapq.heappushpop(heap,-1*num)
        res=[]
        while heap:
            res.append(-1*heapq.heappop(heap))
        return res[::-1]
```