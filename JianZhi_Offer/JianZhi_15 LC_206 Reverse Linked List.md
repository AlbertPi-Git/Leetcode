# JianZhi_11 LC_206 - Reverse Linked List

## Initial idea
Use dummy node to avoid corner case, use prev and current ptr. Remember to remove dummy node at last and return prev (not ptr).
```python
class Solution:
    def ReverseList(self, head):
        if head is None:
            return None
        dummy=ListNode(None)
        dummy.next=head
        prev,ptr=dummy,head
        while ptr:
            tmpNext=ptr.next
            ptr.next=prev
            prev=ptr
            ptr=tmpNext
        head.next=None
        return prev
```