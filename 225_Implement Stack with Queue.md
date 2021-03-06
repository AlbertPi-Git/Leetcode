# Leetcode 225 - Implement Stack with Queue

## Initial Idea
```c++
class MyStack {
private:
    queue<int> q1;
    queue<int> q2;
public:
    /** Initialize your data structure here. */
    MyStack() {

    }
    
    /** Push element x onto stack. */
    void push(int x) {
        if(q2.empty())
            q1.push(x);
        else
            q2.push(x);
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        if(q1.size()){
            int q1_size=q1.size();
            for(int i=0;i<q1_size-1;++i){
                q2.push(q1.front());
                q1.pop();
            }
            int res=q1.front();
            q1.pop();
            return res;
        }else{
            int q2_size=q2.size();
            for(int i=0;i<q2_size-1;++i){
                q1.push(q2.front());
                q2.pop();
            }
            int res=q2.front();
            q2.pop();
            return res;
        }
    }
    
    /** Get the top element. */
    int top() {
        int res=pop();
        if(q1.size()){
            q1.push(res);
        }else{
            q2.push(res);
        }
        return res;
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q1.empty() && q2.empty(); 
    }
};
```

## Improvement
Move the complexity to the push()
```c++
class MyStack {
private:
    std::queue<int> q1;
    std::queue<int> q2;

public:
    /** Initialize your data structure here. */
    MyStack() {

    }
    
    /** Push element x onto stack. */
    void push(int x) {
        if(q1.empty()){
            q1.push(x);
            while(q2.size()){
                q1.push(q2.front());
                q2.pop();
            }
        }else{
            q2.push(x);
            while(q1.size()){
                q2.push(q1.front());
                q1.pop();
            }
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int res;
        if(q1.size()){
            res=q1.front();
            q1.pop();
        }else{
            res=q2.front();
            q2.pop();
        }
        return res;
    }
    
    /** Get the top element. */
    int top() {
        if(q1.size())
            return q1.front();
        else
            return q2.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q1.empty()&&q2.empty();
    }
};
```

## Others' Idea 1
Use one queue is enough.
```c++
class MyStack {
private:
    std::queue<int> q;

public:
    /** Initialize your data structure here. */
    MyStack() {

    }
    
    /** Push element x onto stack. */
    void push(int x) {
        q.push(x);
        int size=q.size();
        for(int i=0;i<size-1;++i){
            q.push(q.front());
            q.pop();
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int res=q.front();
        q.pop();
        return res;
    }
    
    /** Get the top element. */
    int top() {
        return q.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q.empty();
    }
};
```