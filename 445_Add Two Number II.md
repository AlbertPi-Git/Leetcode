# Leetcode 445 - Add Two Number II

## Initial Idea
Can't reverse two LinkedList directly, so use two stacks for assistance.
```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        std::stack<ListNode*> s1;
        std::stack<ListNode*> s2;
        while(l1){
            s1.push(l1);
            l1=l1->next;
        }
        while(l2){
            s2.push(l2);
            l2=l2->next;
        }
        int carry=0;
        ListNode* ptr=new ListNode(0);  //ptr node is used to store the result of current digit
        while(s1.size()||s2.size()||carry){
            int tmpSum=carry;
            if(s1.size()){
                tmpSum+=s1.top()->val;
                s1.pop();
            }
            if(s2.size()){
                tmpSum+=s2.top()->val;
                s2.pop();
            }
            ptr->val=tmpSum%10;
            carry=tmpSum/10;
            ListNode* tmp=new ListNode(0);  //create a new node for higher digit
            tmp->next=ptr;  //connect it with current node
            ptr=tmp;    //set that higher node as current node and prepare for the next iteration
        }
        return ptr->next;   //in the last iteration we still create a new higher node, but then the loop ends, it isn't used. So we need to return ptr->next rather than ptr;
    }
};
```