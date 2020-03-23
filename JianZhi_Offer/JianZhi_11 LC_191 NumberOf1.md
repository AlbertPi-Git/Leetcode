# JianZhi_11 - NumberOf1

## Initial idea
For non-negative integer, just need to bit wise AND with 1 to get the last bit. Keep shifting right until it becomes 0. While for the negative integer, 1 is added to the most significant bit, so can't do the same thing as non-negative number. Instead, we keep shifting right until it becomes -1 and count how many 0 are in the integer. Then use number of 1 in -1 to subtract that number to get the number of 1.

Bits of an integer in python is not fixed, so manually set it as 32bits (which means number of 1 in -1 is 32).
```python
class Solution:
    def NumberOf1(self, n):
        mask=1
        cnt=0
        if n>=0:
            while n!=0:
                cnt+=((n&mask)==1)
                n=n>>1
        else:
            cnt=32
            while(n!=-1):
                cnt-=((n&mask)==0)
                n=n>>1
        return cnt
```

In C++, there isn't such problem.
```c++
class Solution {
public:
     int  NumberOf1(int n) {
         int mask=1;
         int cnt=0;
         if(n>=0){
             while(n!=0){
                 cnt+=((n&mask)==1);
                 n=n>>1;
             }
         }else{
             cnt=(sizeof (int))*8;
             if(n!=-1){
                 while(n!=-1){
                     cnt-=((n&mask)==0);
                     n=n>>1;
                 }
             }
         }
         return cnt;
     }
};
```

## Others' idea 1
N & N-1 can eliminate the 1 on the most right side, so count how many times this operation can be done until N becomes 0 will give the number of 1 in N. This method doesn't require separate consideration of negative number, since the smallest negative number minus 1 will down overflow and becomes the biggest positive number, thus makes N & N-1 becomes 0 and terminate the loop.  

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        cnt=0
        while(n):
            cnt+=1
            n=((n-1)&n)
        return cnt
```

```c++
class Solution {
public:
     int  NumberOf1(int n) {
         int cnt=0;
         while(n){
             cnt++;
             n=(n-1)&n;
         }
         return cnt;
     }
};
```