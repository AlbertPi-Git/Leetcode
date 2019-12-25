# JianZhi_16 LC_21 - Merge Two Sorted Lists

## Initial idea
Use dummy head
```python
class Solution:
    def Merge(self, head1, head2):
        if not head1:
            return head2
        if not head2:
            return head1
        res=ListNode(None)
        ptr=res
        while head1 and head2:
            if head1.val<=head2.val:
                ptr.next=head1
                head1=head1.next
            else:
                ptr.next=head2
                head2=head2.next
            ptr=ptr.next
        if head1:
            ptr.next=head1
        else:
            ptr.next=head2
        return res.next
```