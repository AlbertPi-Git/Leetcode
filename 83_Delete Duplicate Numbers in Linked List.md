# Leetcode 83 - Delete Duplicate Numbers in Linked List

## Initial Idea
```c++
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        if(pHead==nullptr)
            return pHead;
        ListNode* ptr=pHead->next;
        ListNode* prev=pHead;
        while(ptr!=nullptr){
            if(ptr->val==prev->val){
                prev->next=ptr->next;
                ptr=ptr->next;
            }else{
                prev=prev->next;
                ptr=ptr->next;
            }
        }
        return pHead;
    }
};
```