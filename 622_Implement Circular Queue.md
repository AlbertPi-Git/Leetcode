# Leetcode 622 - Implement Circular Queue

## Initial Idea
Remember to change curSize in push and pop. Remember tail always points to the next place of current last element. So Rear() needs to return the element in the (tail+capacity-1)%capacity

```c++
class MyCircularQueue {
private:
    int* buf;
    int capacity;
    int curSize;
    int head;
    int tail;
public:
    /** Initialize your data structure here. Set the size of the queue to be k. */
    MyCircularQueue(int k) {
        buf=new int[k];
        capacity=k;
        curSize=0;
        head=0;
        tail=0;
    }
    
    /** Insert an element into the circular queue. Return true if the operation is successful. */
    bool enQueue(int value) {
        if(curSize<capacity){
            buf[tail]=value;
            tail=(tail+1)%capacity;
            ++curSize;
            return true;
        }else
            return false;
    }
    
    /** Delete an element from the circular queue. Return true if the operation is successful. */
    bool deQueue() {
        if(curSize>0){
            head=(head+1)%capacity;
            --curSize;
            return true;
        }else
            return false;
    }
    
    /** Get the front item from the queue. */
    int Front() {
        if(curSize>0)
            return buf[head];
        else
            return -1;
    }
    
    /** Get the last item from the queue. */
    int Rear() {
        if(curSize>0)
            return buf[(tail+capacity-1)%capacity];
        else
            return -1;
    }
    
    /** Checks whether the circular queue is empty or not. */
    bool isEmpty() {
        return curSize==0;
    }
    
    /** Checks whether the circular queue is full or not. */
    bool isFull() {
        return curSize==capacity;
    }
};
```