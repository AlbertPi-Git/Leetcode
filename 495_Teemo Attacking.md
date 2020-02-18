# Leecode 495 - Teemo Attacking

https://leetcode-cn.com/problems/teemo-attacking

## Initial Idea

```c++
class Solution {
public:
    int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        int res=0;
        for(int i=0;i<timeSeries.size();i++){
            if(i+1<timeSeries.size()){
                if(timeSeries[i+1]-timeSeries[i]>=duration){
                    res+=duration;
                }else{
                    res+=timeSeries[i+1]-timeSeries[i];
                }
            }else{
                res+=duration;
            }
        }
        return res;
    }
};
```

## Improvement
```c++
class Solution {
public:
    int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        if(!timeSeries.size())
            return 0;
        int res=duration;
        int endTime=timeSeries[0]+duration;
        for(int i=1;i<timeSeries.size();i++){
            if(timeSeries[i]<endTime){
                res+=(timeSeries[i]-timeSeries[i-1]);
            }else{
                res+=duration;
            }
            endTime=timeSeries[i]+duration;
        }
        return res;
    }
};
```

Or

```c++
class Solution {
public:
    int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        if(!timeSeries.size())
            return 0;
        int res=0;
        int endTime=timeSeries.front();
        timeSeries.push_back(timeSeries.back()+duration);
        for(int i=0;i<timeSeries.size()-1;i++){
            if(timeSeries[i]<=endTime && timeSeries[i+1]>endTime){
                res+=(duration-endTime+timeSeries[i]);
                endTime=timeSeries[i]+duration;
            }else if(timeSeries[i]>endTime){
                res+=duration;
                endTime=timeSeries[i]+duration;
            }
        }
        return res;
    }
};
```

## Others' Idea 1
Simpler but slower
```c++
class Solution {
public:
    int findPoisonedDuration(vector<int>& timeSeries, int duration) {
        if(!timeSeries.size())
            return 0;
        int res=0;
        for(int i=0;i<timeSeries.size()-1;i++){
            res+=min(timeSeries[i+1]-timeSeries[i],duration);
        }
        res+=duration;
        return res;
    }
};
```