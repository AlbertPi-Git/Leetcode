# JianZhi_21 LC_946 - Validate Stack Sequence

## Initial idea (Didn't completed)
Try to enumerate all possible pop sequences according to push sequence using DFS, but didn't be able to enumerate all possibilities. Even if it can be done, it would TLE.

```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        res=[]
        def dfs(pushV,stack,buf):
            if len(pushV)==0:
                res.append(buf)
            for i in range(1,len(pushV)+1):

                dfs(pushV[i:],buf+pushV[:i][-1::-1])
        dfs(pushV,[],[])
        for res_i in res:
            print(res_i)
        if popV in res:
            return True
        else:
            return False
```

## Others' idea 1
Simulate the stack processing, use a stack and push all elements in push sequence order. Only when element in pop sequence is on the top of stack, it can be popped. If the pop sequence is wrong, the stack won't be empty at the end.
```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stack=[]
        popIndex=0
        for num in pushed:
            stack.append(num)
            while popIndex<len(popped) and stack and stack[-1]==popped[popIndex]:
                stack.pop()
                popIndex+=1
        return not stack
```