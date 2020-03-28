# Leetcode 232 - Implement Queue with Two Stacks

## Initial Idea
The main stack store values in input order. Cons: Replicate in pop() and peek()
```c++
class MyQueue {
private:
    std::vector<int> stack1;
    std::vector<int> stack2;
public:
    /** Initialize your data structure here. */
    MyQueue() {

    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        stack1.push_back(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        while(stack1.size()){
            stack2.push_back(stack1.back());
            stack1.pop_back();
        }
        int res=stack2.back();
        stack2.pop_back();
        while(stack2.size()){
            stack1.push_back(stack2.back());
            stack2.pop_back();
        }
        return res;
    }
    
    /** Get the front element. */
    int peek() {
        while(stack1.size()){
            stack2.push_back(stack1.back());
            stack1.pop_back();
        }
        int res=stack2.back();
        // stack2.pop_back();
        while(stack2.size()){
            stack1.push_back(stack2.back());
            stack2.pop_back();
        }
        return res;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return stack1.empty();
    }
};
```

## Others' Idea 1
The main stack store values in the reverse order, oldest on the top.
```c++
class MyQueue {
private:
    std::stack<int> s1;
    std::stack<int> s2;
public:
    /** Initialize your data structure here. */
    MyQueue() {

    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        while(s1.size()){
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(x);
        while(s2.size()){
            s1.push(s2.top());
            s2.pop();
        }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int res=s1.top();
        s1.pop();
        return res;
    }
    
    /** Get the front element. */
    int peek() {
        return s1.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return s1.empty();
    }
};
```