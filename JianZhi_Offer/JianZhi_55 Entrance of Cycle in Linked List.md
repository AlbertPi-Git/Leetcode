# JianZhi 55 - Entrance of Cycle in Linked List

## Initial Idea
```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow=head;
        ListNode* fast=head;
        while(fast!=nullptr && fast->next!=nullptr){
            fast=fast->next->next;
            slow=slow->next;
            if(fast==slow)
                break;
        }
        if(fast==nullptr||fast->next==nullptr){
            return nullptr;
        }else{
            slow=head;
            while(fast!=slow){
                fast=fast->next;
                slow=slow->next;
            }
            return fast;
        }
    }
};
```