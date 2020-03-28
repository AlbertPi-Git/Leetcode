# Leetcode 21 - Merge Two Sorted Linked List

## Initial Idea
Just remember to move ptr,l1,l2 to next. And return the next of dummy.
```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy=new ListNode(-1);
        ListNode* ptr=dummy;
        while(l1&&l2){
            if(l1->val<=l2->val){
                ptr->next=l1;
                l1=l1->next;
            }else{
                ptr->next=l2;
                l2=l2->next;
            }
            ptr=ptr->next;
        }
        if(l1){
            ptr->next=l1;
            l1=nullptr;
        }else{
            ptr->next=l2;
            l2=nullptr;
        }
        return dummy->next;
    }
};
```
