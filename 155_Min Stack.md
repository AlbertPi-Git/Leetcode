# Leetcode 155 - Min Stack

## Initial Idea
Use another stack to store history mins.
```c++
class MinStack {
private:
    std::stack<int> s1;
    std::stack<int> s2;

public:
    MinStack(){}
    
    void push(int x) {
        if(s1.empty()){
            s1.push(x);
            s2.push(x);
        }else{
            s1.push(x);
            if(x<=s2.top()){
                s2.push(x);
            }
        }
    }
    
    void pop() {
        if(s1.empty())
            return;
        if(s1.top()==s2.top())
            s2.pop();
        s1.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int getMin() {
        return s2.top();
    }
};
```

## Use Doubly LinkedList Implement Stack
```c++
struct Node{
    int val;
    Node* prev;
    Node* next;
    Node(int val_):val(val_),prev(nullptr),next(nullptr){}
};

class MinStack {
private:
    Node* sHead1;
    Node* sHead2;
    int size;

public:
    MinStack():sHead1(nullptr),sHead2(nullptr),size(0){}
    
    void push(int x) {
        if(0==size){
            sHead1=new Node(x);
            sHead2=new Node(x);
        }else{
            if(x<=sHead2->val){
                sHead2->next=new Node(x);
                sHead2->next->prev=sHead2;
                sHead2=sHead2->next;
            }
            sHead1->next=new Node(x);
            sHead1->next->prev=sHead1;
            sHead1=sHead1->next;
        }
        ++size;
    }
    
    void pop() {
        if(0==size)
            return;
        if(sHead1->val==sHead2->val){
            Node* tmp=sHead2;
            sHead2=sHead2->prev;
            delete tmp;
            tmp=nullptr;
        }
        Node* tmp=sHead1;
        sHead1=sHead1->prev;
        delete tmp;
        tmp=nullptr;
        --size;
    }
    
    int top() {
        return sHead1->val;
    }
    
    int getMin() {
        return sHead2->val;
    }
};
```

## Others' Idea 1
Don't use another stack, but rather store the previous min with current one if current one is the new min.
```c++
class MinStack {
private:
    std::stack<int> s1;
    int min;

public:
    MinStack(){}
    
    void push(int x) {
        if(s1.empty()){ //Initial case, push and set it as min
            s1.push(x); 
            min=x;
        }else{
            if(x<=min){ 
                s1.push(min);   //If this one is smaller than curren min, then put the current min under this one in stack as the previous min. And set current one as new min.
                min=x;
            }
            s1.push(x);
        }
    }
    
    void pop() {
        if(s1.empty())
            return;
        if(s1.size()==1)    //If there is only one left, then it should be the first push one, it doesn't have previous min, so pop only once.
            s1.pop();
        else if(s1.top()==min){     //If current min gonna be popped
            s1.pop();       // Firstly pop the current min
            min=s1.top();   // The previous min is under it, so set that as the current min
            s1.pop();       // But this previous mean is a fake one, not real data, so also pop it
        }else
            s1.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int getMin() {
        return min;
    }
};
```
