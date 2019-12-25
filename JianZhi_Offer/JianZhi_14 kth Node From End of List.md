# JianZhi_14 - kth Node From End of the List

## Initial idea
Two pointers k away, remember to handle k==0 and k>len cases.
```python
class Solution:
    def FindKthToTail(self, head, k):
        if k==0:
            return None
        ptr=head
        for i in range(k):
            if ptr is None:
                return None
            ptr=ptr.next
        while ptr:
            ptr=ptr.next
            head=head.next
        return head
```
