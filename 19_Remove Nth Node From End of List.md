# Leetcode 19 - Remove Nth Node From End of List

## Initial idea
Use two pointers that are k away, and use prev to do the remove. And use dummy node to avoid considering corner case where head is removed.
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, k: int) -> ListNode:
        dummy=ListNode(None)
        dummy.next=head
        ptr1,ptr2=head,head
        prev=dummy
        for i in range(k):
            ptr1=ptr1.next
        while ptr1:
            ptr1=ptr1.next
            ptr2=ptr2.next
            prev=prev.next
        prev.next=ptr2.next
        return dummy.next
```