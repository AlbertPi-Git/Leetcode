# Leetcode 206 - Reverse Linked List

## Initial Idea
Iterative
```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==nullptr)
            return head;
        ListNode* ptr1=head;
        ListNode* ptr2=head->next;
        while(ptr2!=nullptr){
            ListNode* tmpNext=ptr2->next;
            ptr2->next=ptr1;
            ptr1=ptr2;
            ptr2=tmpNext;
        }
        head->next=nullptr; //very important, break the circle
        return ptr1;    //when ptr2 reach nullptr, ptr1 points to the last element in the original list, thus the new head
    }
};
```

Recursive
```c++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head==nullptr||head->next==nullptr)
            return head;
        ListNode* subHead=reverseList(head->next);  //recursively reverse the sublist start from next element
        ListNode* subTail=head->next;   //head still points to the subsequent element in the original list, which now is the tail the new sublist.
        subTail->next=head;     
        head->next=nullptr;     //break the circle
        return subHead;
    }
};
```