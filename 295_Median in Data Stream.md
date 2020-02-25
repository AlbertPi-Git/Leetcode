# Leetcode 295 - Median in Data Stream

## Others' Idea 1
```c++
class MedianFinder {
public:
    /** initialize your data structure here. */
    priority_queue<int> MaxHeap;
    priority_queue<int,vector<int>,greater<int>> MinHeap;

    MedianFinder() {

    }
    
    void addNum(int num) {
        if(MaxHeap.empty()){
            MaxHeap.push(num);
        }else{
            if(MaxHeap.size()==MinHeap.size()){
                if(num<=MinHeap.top())
                    MaxHeap.push(num);
                else{
                    MaxHeap.push(MinHeap.top());
                    MinHeap.pop();
                    MinHeap.push(num);
                }
            }else{
                if(num>=MaxHeap.top())
                    MinHeap.push(num);
                else{
                    MinHeap.push(MaxHeap.top());
                    MaxHeap.pop();
                    MaxHeap.push(num);
                }
            }
        }
    }
    
    double findMedian() {
        if(MaxHeap.size()>MinHeap.size())
            return MaxHeap.top();
        else
            return ((double)MaxHeap.top()+(double)MinHeap.top())/2;
    }
};
```