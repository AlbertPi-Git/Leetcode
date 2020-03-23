# Leetcode 2 - Add Two Number

## Initial idea
Big integer addition in linked list, keep create new node and link it to res as long as l1 or l2 or c is valid. 

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        c=0
        dummy=ListNode(None)
        res=dummy
        while l1 or l2 or c:
            val1=l1.val if l1 else 0
            val2=l2.val if l2 else 0
            res.next=ListNode((val1+val2+c)%10)
            c=(val1+val2+c)//10
            if l1:
                l1=l1.next
            if l2:
                l2=l2.next
            res=res.next
        return dummy.next
```

## Improvement
No need to create new node if one of l1, l2's node is valid.

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        c=0
        dummy=ListNode(None)
        res=dummy
        while l1 or l2 or c:
            val1=l1.val if l1 else 0
            val2=l2.val if l2 else 0
            if l1:
                res.next=l1
                res.next.val=(val1+val2+c)%10
            elif l2:
                res.next=l2
                res.next.val=(val1+val2+c)%10
            else:
                res.next=ListNode(c)
            c=(val1+val2+c)//10
            if l1:
                l1=l1.next
            if l2:
                l2=l2.next
            res=res.next
        return dummy.next
```