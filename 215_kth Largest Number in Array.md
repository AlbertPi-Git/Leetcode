# Leetcode 215- Kth Largest Number in Array

## Initial Idea
Using MinHeap, using MinHeap to contain largest K number, then after going through all numbers, the top of the heap is the kth largest number.
```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int,vector<int>,greater<int>> MinHeap;
        for(auto& num:nums){
            if(MinHeap.size()<k)
                MinHeap.push(num);
            else{
                if(num>MinHeap.top()){
                    MinHeap.pop();
                    MinHeap.push(num);
                }
            }
        }
        return MinHeap.top(); 
    }
};
```