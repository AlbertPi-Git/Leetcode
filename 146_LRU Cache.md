# Leetcode 146 - LRU Cache

## Initial idea
Use ordered dictionary to keep the inserting order, every time 'get' successfully, move it to the end of dic (the front is the oldest one). Every time key of 'put' is already in the dic, move to the end then update value. If key of 'put' is not in the dic: directly add to dic if dic is not full, else remove the oldest one then add it to the dic.
```python
from collections import OrderedDict
class LRUCache:

    def __init__(self, capacity: int):
        self.dic=OrderedDict()
        self.capacity=capacity

    def get(self, key: int) -> int:
        if key in self.dic:
            self.dic.move_to_end(key)   # move_to_end's default is 'last=False', so default is moving to the end of the dic
            return self.dic[key]
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.dic:
            self.dic[key]=value
            self.dic.move_to_end(key)
        else:
            if len(self.dic)<self.capacity:
                self.dic[key]=value
            else:
                self.dic.popitem(last=False)    #popitem's default is 'last=True', so the last one is popped
                self.dic[key]=value
```

## Implement the orderedDict
Use hashmap + doubly linked list to implement the orderedDict, hashmap guarantees that the search can be done in O(1) time and doubly linked list makes sure that insert, remove, move to the end can be done in O(1) time.
```python
class ListNode:
    def __init__(self,key,value):
        self.key=key
        self.value=value
        self.prev=None
        self.next=None

class OrderedDict:
    def __init__(self):
        self.dic=dict()
        self.dummy=ListNode(None,None)
        self.tail=self.dummy
    
    def size(self):
        return len(self.dic)

    def inDic(self,key):
        return key in self.dic

    def put(self,key,value):
        newNode=ListNode(key,value)
        self.tail.next=newNode
        newNode.prev=self.tail
        self.tail=self.tail.next
        self.dic[key]=newNode
        return 
    
    def pop(self):
        toDelNode=self.dummy.next
        self.dummy.next=toDelNode.next
        if self.tail!=toDelNode:
            self.dummy.next.prev=self.dummy
        del self.dic[toDelNode.key]
        return

    def get(self,key):
        return self.dic[key].value
    
    def moveToEnd(self,key,value):
        toMoveNode=self.dic[key]
        toMoveNode.key=key
        toMoveNode.value=value
        if self.tail==toMoveNode:
            return
        toMoveNode.prev.next=toMoveNode.next
        toMoveNode.next.prev=toMoveNode.prev
        self.tail.next=toMoveNode
        toMoveNode.prev=self.tail
        self.tail=self.tail.next
        return

class LRUCache:

    def __init__(self, capacity: int):
        self.dic=OrderedDict()
        self.capacity=capacity

    def get(self, key: int) -> int:
        if self.dic.inDic(key):
            res=self.dic.get(key)
            self.dic.moveToEnd(key,res)
            return res
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if self.dic.size()==self.capacity and self.dic.inDic(key)==False:
            self.dic.pop()
            self.dic.put(key,value)
        if self.dic.inDic(key):
            self.dic.moveToEnd(key,value)
        else:
            self.dic.put(key,value)
```