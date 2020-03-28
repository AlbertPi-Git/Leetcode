# Linked List Cycle 2

## Initial Idea
Use fast and slow ptr to find whether there is a cycle, and the node when they meet if there is a cycle. Then according to the geometry, we know that if two ptr start from head and meet node, they will meet at the node where the cycle begins.

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        fast,slow=head,head
        while fast!=None and fast.next!=None:
            fast=fast.next.next
            slow=slow.next
            if fast==slow:
                break
        if fast==None or fast.next==None:
            return None
        else:
            slow=head
            while fast!=slow:
                fast=fast.next
                slow=slow.next
            return slow
```

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast=head;
        ListNode* slow=head;
        while(fast!=nullptr && fast->next!=nullptr){
            fast=fast->next->next;
            slow=slow->next;
            if(slow==fast)      // can't put this into while() since slow==fast at the beginning, but also can't use (slow!=fast||fast==head) to avoid this problem since it will cause endless loop if entrance of cycle is the head.
                break;
        }
        if(fast==nullptr || fast->next==nullptr)
            return nullptr;
        slow=head;
        while(fast!=slow){
            fast=fast->next;
            slow=slow->next;
        }
        return slow;
    }
};
```

Use dummy node can solve the above problem and make if(slow==fast&&slow!=dummy) can be put at the beginning of the loop
```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* fast=dummy;
        ListNode* slow=dummy;
        while(fast&&fast->next){
            if(slow==fast&&slow!=dummy)
                break;
            fast=fast->next->next;
            slow=slow->next;
        }
        if(!fast||!fast->next)
            return nullptr;
        slow=dummy;
        while(slow!=fast){
            slow=slow->next;
            fast=fast->next;
        }
        return slow;
    }
};
```