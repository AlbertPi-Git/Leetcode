# JianZhi 56 - Remove All Dupicates in Sorted Linked List

Note that the first one is also removed, e.g. 1->2->2->3 becomes 1->3

## Initial Idea
```c++
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        if(pHead==nullptr||pHead->next==nullptr)
            return pHead;
        ListNode* dummy=new ListNode(-1);
        dummy->next=pHead;
        ListNode* prev=dummy;
        ListNode* ptr1=pHead;
        ListNode* ptr2=pHead->next;
        while(ptr2!=nullptr){
            if(ptr2->val==ptr1->val){
                while(ptr2!=nullptr&&ptr2->val==ptr1->val){
                    ptr2=ptr2->next;
                }
                prev->next=ptr2;
                ptr1=ptr2;
                if(ptr2)
                    ptr2=ptr2->next;
            }else{
                prev=prev->next;
                ptr1=ptr1->next;
                ptr2=ptr2->next;
            }
        }
        return dummy->next;
    }
};
```
