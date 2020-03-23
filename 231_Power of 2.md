# Leetcode 231 - Power of 2

https://leetcode-cn.com/problems/power-of-two/

## Initial Idea
Use x&(x-1) to get rid of the most right 1 bit in the bit sequence, if x&(x-1)==0, then return true, else return false.
```c++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n<=0)
            return false;
        unsigned int res=n;
        return !(res&(res-1));
    }
};
```