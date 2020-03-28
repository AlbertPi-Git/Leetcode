# Leetcode 202 - Happy Number

## Initial Idea
Assume that unhappy number will fall into a loop that doesn't contain 1. So we can use a set to record all numbers on this chain. Then the chain of happy number is a circle, when we find the same number in the set, we know it's unhappy number.
```c++
class Solution {
public:
    bool isHappy(int n) {
        std::unordered_set<int> hashSet;
        hashSet.insert(n);
        while(n!=1){
            int sum=0;
            while(n>0){
                sum+=(n%10)*(n%10);
                n=n/10;
            }
            if(hashSet.find(sum)!=hashSet.end())
                return false;
            else{
                n=sum;
                hashSet.insert(n);
            }
        }
        return true;
    }
};
```

## Optimization
We can manually compute first N integers are happy numbers or not, then relax the loop termination condition, thus, accelerate the computation.