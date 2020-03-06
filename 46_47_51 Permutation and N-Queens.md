# Leetcode 46, 47, 51 Permutation I, II and N-Queens

These three problems all use backtrack algorithms, so put them together here. The basic framework of back track algorithm is:
```python
def backtrack(avail_list,cur_path):
    if reach termination condition:
        res.append(cur_path)
    for choice in avail_list:
        make decision #i.e. choose a decision from avail_list and add it to cur_path
        backtrack(avail_list,cur_path)
        restore path # have to restore this decision, or it will mess up next decision
```
## Permutation I
Simple permutation problem where every number is unique.

### Basic Framework
Implementation of basic framework above.
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res=[]
        def backtrack(nums,path):
            if len(path)==len(nums):
                res.append(path[:]) # Need to append a copy of path, since later operations will modify this list
            for num in nums:
                if num in path:
                    continue
                path.append(num)
                backtrack(nums,path)
                path.pop()
        backtrack(nums,[])
        return res
```

### My initial idea
Slice and copy the list to shrink avail_list, copy and add current choice to path for next backtrack. This implementation doesn't require explicit 'make choice' and 'restore path' since all parameters send to the next backtrack are copied. It should use more memory, but actually its memory utilization is better than the basic framework.
```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res=[]
        def backtrack(nums,path):
            if not nums and path:
                res.append(path)
            for i in range(len(nums)):
                backtrack(nums[:i]+nums[i+1:],path+[nums[i]])
        backtrack(nums,[])
        return res
```

### Another Idea
```c++
void perm(int list[], int k, int m)
{
    if (k==m)
    {
        copy(list,list+m,ostream_iterator<int>(cout," "));
        cout<<endl;
        return;
    }
 
    for (int i=k; i<m; i++)
    {
        swap(list[k],list[i]);
        perm(list,k+1,m);
        swap(list[k],list[i]);
    }
}
```

## Permutation II

## My initial idea
There maybe duplicate numbers in the list, so codes in Permutation I will produce some duplicate results. To tackle this problem, we firstly sort the list (if in case the origin list is not sorted). Thus, all duplicate numbers will be adjacent. Then in the backtracking, we only choose the first one in those duplicate numbers, so that there won't be duplicates in results.
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

## Basic Framework
If there are duplicate numbers, can't use 'num in path' to implicitly decide whether this number can be chosen. Use explicit used list to mark used number instead. Also only choose the first one in adjacent duplicates.
```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        res=[]
        nums.sort()
        def backtrack(s,path,used):
            if len(path)==len(s):
                res.append(path[:])
            for i in range(len(s)):
                if (i>0 and s[i]==s[i-1] and used[i-1]==0) or used[i]==1:   
                    continue
                path.append(s[i])
                used[i]=1
                backtrack(s,path,used)
                path.pop()
                used[i]=0
        backtrack(nums,[],[0]*len(nums))
        return res
```

## N-Queens
### Initial idea
Use the basic framework of backtracking. The structure of backtracking function is clear but need to figure out the condition that Queens won't attack each other.

To avoid each Queen attacking each other, they should not in same row or column or diagonal or anti-diagonal. Not in same row is naturally guaranteed since we iterate through rows. It's easy to check whether they are in the same row using 'usedColumn' to hold previously occupied columns. For diagonal and anti-diagonal, if they are in the same diagonal, then the difference of their row index and column index is the same. If they are in the same anti-diagonal, the sum of their row index and column index are the same. So we use 'usedDiff' and 'usedSum' to hold previously occupied diagonal and anti-diagonal.   
```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        res=[]
        def backtrack(row,usedColumn,usedDiff,usedSum,config):
            if row==n:
                print(config)
                pattern=[['.']*n for _ in range(n)]
                for i in range(len(config)):
                    pattern[i][config[i]]='Q'
                    pattern[i]=''.join(pattern[i])
                res.append(pattern)
            for i in range(n):
                Diff,Sum=row-i,row+i
                if i in usedColumn or Diff in usedDiff or Sum in usedSum:
                    continue
                usedColumn.append(i)
                usedDiff.append(Diff)
                usedSum.append(Sum)
                config.append(i)
                backtrack(row+1,usedColumn,usedDiff,usedSum,config)
                usedColumn.pop()
                usedDiff.pop()
                usedSum.pop()
                config.pop()
        backtrack(0,[],[],[],[])    
        return res
```