# JianZhi_28 - Find More Than Half

## Initial idea
Use hash map to store the how many times each number appear. Return the number if counter>len(numbers). Time complexity O(N), space complexity in worse case is O(N).

```python
from collections import defaultdict
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        dic=defaultdict(int)
        for num in numbers:
            dic[num]+=1
            if dic[num]>len(numbers)/2:
                return num
        return 0
```

## Moore Algorithm
Space complexity is O(1), time complexity is O(2N). Don't need to store the appear times of each number, rather, only store the current candidate and its counter. Go through the list, if current number if the same with candidate, then increment the number else decrement the number. If counter==0, set the current number as candidate and counter=1. 

If there is indeed a number appears over half of times, then after the going through, the candidate will naturally be that number. However, if there isn't such number, the information obtained during the first going through can't tell us that. Thus, have to go through the list again and count how many times does the final candidate appear. If it's indeed greater than half of length of the list, then return it else return 0.

```python
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        if not numbers:
            return 0
        candidate=numbers[0]
        counter=1
        for i in range(1,len(numbers)):
            if numbers[i]==candidate:
                counter+=1
            else:
                if counter==0:
                    candidate=numbers[i]
                    counter=1
                else:
                    counter-=1
        counter=0
        for num in numbers:
            if num==candidate:
                counter+=1
        return candidate if counter>len(numbers)/2 else 0
```