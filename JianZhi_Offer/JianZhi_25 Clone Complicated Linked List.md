# JianZhi_25 - Clone Complicated LinkedList

Each node of a complicated linked list contains 1. label 2. next pointer 3. random pointer. Given a head node of complicated linked list, clone the whole list and return a new head.

## Initial idea
Firstly, clone the main chain of linked list (i.e. those linked by next pointer). Then clone the random pointer relation. To clone the random relations, my initial idea is to search from the beginning for each node. This can work even if the label of each node is not unique, but time complexity is O(N^2).

```python
class Solution:
    def Clone(self, head):
        if not head:
            return None
        res=RandomListNode(head.label)
        ptr_old,ptr_clone=head,res
        while ptr_old.next:
            ptr_clone.next=RandomListNode(ptr_old.next.label)
            ptr_old=ptr_old.next
            ptr_clone=ptr_clone.next
        
        ptr_old,ptr_clone=head,res
        while ptr_old:
            if ptr_old.random:
                ptr1,ptr2=head,res
                while ptr1!=ptr_old.random:
                    ptr1=ptr1.next
                    ptr2=ptr2.next
                ptr_clone.random=ptr2
            ptr_old=ptr_old.next
            ptr_clone=ptr_clone.next
        return res
```

## Improvement
If the label of each node is unique (true for this problem), can use hash map to store and search the node so that time complexity is O(N). But this method is not universal.
```python
class Solution:
    def Clone(self, head):
        if not head:
            return None
        res=RandomListNode(head.label)
        dic={res.label:res}
        ptr_old,ptr_clone=head,res
        while ptr_old.next:
            ptr_clone.next=RandomListNode(ptr_old.next.label)
            dic[ptr_clone.next.label]=ptr_clone.next
            ptr_old=ptr_old.next
            ptr_clone=ptr_clone.next
        
        ptr_old,ptr_clone=head,res
        while ptr_old:
            if ptr_old.random:
                ptr_clone.random=dic[ptr_old.random.label]
            ptr_old=ptr_old.next
            ptr_clone=ptr_clone.next
        return res
``` 

## Others' idea 1
Placing the cloned node after the original node when clone the main chain. Since the cloned node is adjacent to the original one, thus, nodes pointed by the same random pointer are also adjacent. So it's much easier to clone those random pointer relations. This method doesn't require unique labels and time complexity is O(N).
```python
class Solution:
    def Clone(self, head):
        if not head:
            return None
        ptr_old,ptr_clone=head,None
        while ptr_old:
            old_next=ptr_old.next       #keep next
            ptr_clone=RandomListNode(ptr_old.label)     #create clone node
            ptr_old.next=ptr_clone      #set the next of current original node to clone node
            ptr_clone.next=old_next     #set the next of the clone node to next in the original list

            ptr_old=old_next            #move original pointer to next in original list
            ptr_clone=None              #this line is not necessary, but adding it makes code symmetric
        
        ptr_old=head            
        while ptr_old:                  #Clone random pointer relations
            if ptr_old.random:          
                ptr_old.next.random=ptr_old.random.next     #random of clone node is the next of random of current original node
            ptr_old=ptr_old.next.next       #move to next original node
        
        res=RandomListNode(None)        #dummy node
        ptr_clone=res
        ptr_old=head
        while ptr_old:                  #separate the clone list from the original one
            ptr_clone.next=ptr_old.next
            old_next=ptr_old.next.next
            ptr_old.next=None
            
            ptr_old=old_next
            ptr_clone=ptr_clone.next
            
        return res.next
``` 