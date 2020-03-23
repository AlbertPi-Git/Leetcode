# JianZhi_3 Print Linked List Reversely


```python
class Solution:
    def printListFromTailToHead(self,listNode):
        res=[]
        while listNode:
            res.append(listNode.val)
            listNode=listNode.next
        res.reverse()
        return res
```

Note: .reverse() and .sort() are in-place operations