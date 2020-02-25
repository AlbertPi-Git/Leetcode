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
            if(slow==fast)
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