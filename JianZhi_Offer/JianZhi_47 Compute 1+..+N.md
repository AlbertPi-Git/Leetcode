# JianZhi 47 - Compute 1+..+N

https://leetcode-cn.com/problems/qiu-12n-lco

## Initial Idea
Can't use * then math formula of 1+..+N is prohibited. Can't use for, while then loop compting is prohibited. Then the only approach left is recursion. But how to check the termination condition if if...else... and ? : can't be used?

## Others' Idea
Use the inherent property of && expression: if A&&B, A==false, then the expression will directly generate 0, expression B won't be computed. Thus, we can use this property to avoid entering recursion function again when n==0.

```c++
class Solution {
public:
    int sumNums(int n) {
        n&&(n+=sumNums(n-1));
        return n;
    }
};
```