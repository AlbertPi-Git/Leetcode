# Leetcode 641 - Implement Circular Deque

## Initial Idea
Tail points to next back available position, head points to next front available position.
```c++
class MyCircularDeque {
private:
    int* buf;
    int curSize;
    int capacity;
    int head;
    int tail;
public:
    /** Initialize your data structure here. Set the size of the deque to be k. */
    MyCircularDeque(int k) {
        buf=new int[k];
        curSize=0;
        capacity=k;
        head=k-1;
        tail=0;
    }
    
    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    bool insertFront(int value) {
        if(curSize<capacity){
            buf[head]=value;
            head=(head-1+capacity)%capacity;
            ++curSize;
            return true;
        }else
            return false;
    }
    
    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    bool insertLast(int value) {
        if(curSize<capacity){
            buf[tail]=value;
            tail=(tail+1)%capacity;
            ++curSize;
            return true;
        }else
            return false;
    }
    
    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    bool deleteFront() {
        if(curSize>0){
            head=(head+1)%capacity;
            --curSize;
            return true;
        }else
            return false;
    }
    
    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    bool deleteLast() {
        if(curSize>0){
            tail=(tail-1+capacity)%capacity;
            --curSize;
            return true;
        }else{
            return false;
        }
    }
    
    /** Get the front item from the deque. */
    int getFront() {
        if(curSize>0)
            return buf[(head+1)%capacity];
        else
            return -1;
    }
    
    /** Get the last item from the deque. */
    int getRear() {
        if(curSize>0)
            return buf[(tail-1+capacity)%capacity];
        else
            return -1;
    }
    
    /** Checks whether the circular deque is empty or not. */
    bool isEmpty() {
        return curSize==0;
    }
    
    /** Checks whether the circular deque is full or not. */
    bool isFull() {
        return curSize==capacity;
    }
};
```