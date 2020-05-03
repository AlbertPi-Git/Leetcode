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

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry=0;
        ListNode dummy(-1);
        ListNode* ptr=&dummy;
        while(l1||l2||carry){
            int tmpSum=carry;
            if(l1){
                tmpSum+=l1->val;
                l1=l1->next;
            }
            if(l2){
                tmpSum+=l2->val;
                l2=l2->next;
            }
            ptr->next=new ListNode(tmpSum%10);
            ptr=ptr->next;
            carry=tmpSum/10;
        }
        return dummy.next;
    }
};
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

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int carry=0;
        ListNode dummy(-1);
        ListNode* ptr=&dummy;
        while(l1||l2||carry){
            int val1=0,val2=0;
            if(l1)val1=l1->val;
            if(l2)val2=l2->val;
            int tmpSum=carry+val1+val2;
            if(l1){
                ptr->next=l1;
                l1->val=tmpSum%10;
            }
            else if(l2){
                ptr->next=l2;
                l2->val=tmpSum%10;
            }else{
                ptr->next=new ListNode(tmpSum%10);
            }
            carry=tmpSum/10;
            ptr=ptr->next;
            if(l1)
                l1=l1->next;
            if(l2)
                l2=l2->next;
        }
        return dummy.next;
    }
};
```