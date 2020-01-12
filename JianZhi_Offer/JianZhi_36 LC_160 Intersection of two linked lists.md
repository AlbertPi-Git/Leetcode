# JianZhi_36 LC_160 - Intersection of Two Linked Lists

## Initial idea 1
Traverse two linked lists at the same time, find the longer one and count how many more nodes does it have than shorter one. Then at the second traverse, move the ptr on the longer one N ahead the shorter one before starting traversing two linked list at the same time. When they met, they will be at the intersection.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, head1: ListNode, head2: ListNode) -> ListNode:
        dummy1,dummy2=ListNode(None),ListNode(None)
        dummy1.next,dummy2.next=head1,head2
        ptr1,ptr2=dummy1,dummy2
        while ptr1 and ptr2:
            ptr1=ptr1.next
            ptr2=ptr2.next
        cnt=0
        if ptr1:
            longerOne=dummy1
            shorterOne=dummy2
            while ptr1:
                cnt+=1
                ptr1=ptr1.next
        else:
            longerOne=dummy2
            shorterOne=dummy1
            while ptr2:
                cnt+=1
                ptr2=ptr2.next
        for i in range(cnt):
            longerOne=longerOne.next
        while longerOne!=shorterOne:
            longerOne=longerOne.next
            shorterOne=shorterOne.next
        return shorterOne
```

## Initial idea 2
Use hash set to store node in linked list 1 in first traversal, then traverse linked list 2, if the node in list 2 is already in hash set, that's the intersection node.
```python
class Solution:
    def getIntersectionNode(self, head1: ListNode, head2: ListNode) -> ListNode:
        ptr1,ptr2=head1,head2
        Set1,Set2=set(),set()
        
        while ptr1:
            if ptr1:
                Set1.add(ptr1)
                ptr1=ptr1.next
        
        while ptr2:
            if ptr2 in Set1:
                return ptr2
            ptr2=ptr2.next
        return None
```

## Others' idea 1
Very like initial idea 1, but instead of figuring out which one is the longer one and how many more nodes does it have, we can redirect ptr1 to head2 when ptr1 reaches None, and the same to ptr2, so that their difference is naturally compensated.

```python
class Solution:
    def getIntersectionNode(self, head1: ListNode, head2: ListNode) -> ListNode:
        dummy1,dummy2=ListNode(None),ListNode(None)
        dummy1.next,dummy2.next=head1,head2
        ptr1,ptr2=dummy1,dummy2
        while ptr1!=ptr2:
            if ptr1==None:
                ptr1=dummy2
            if ptr2==None:
                ptr2=dummy1
            ptr1=ptr1.next
            ptr2=ptr2.next
        return ptr1
```
