# JianZhi 51 - Product Array

## Initial Idea
Brutal force, TLE

## Others' Idea 1
Compute left product and right product for each position once.
```c++
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        int len=a.size();
        vector<int>* res=new vector<int> (len);
        vector<int> left(len);
        for(int i=0;i<len;++i){
            left[i]=i==0?1:left[i-1]*a[i-1];
        }
        vector<int> right(len);
        for(int i=len-1;i>=0;--i){
            right[i]=i==len-1?1:right[i+1]*a[i+1];
        }
        for(int i=0;i<len;++i){
            (*res)[i]=left[i]*right[i];
        }
        return (*res);
    }
};
```