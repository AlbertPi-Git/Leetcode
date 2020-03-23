# JianZhi 48 - Computing Addition with Binary Operation

## Others Idea 1
Bitwise XOR of two numbers can give the remainder of each bit after addition, while the bitwise AND left shift 1 can give the carry received by each bit after addition. Adding A, B means firstly compute bitwise remainder of A+B, then compute bitwise carry of A+B, then add the remainder and carry to obtain the result of A+B. However, we can't use addition, so we can iteratively do XOR and AND <<1 to substitute addition. The process ends when the carry of all bits are 0.

```c++
class Solution {
public:
    int add(int a, int b) {
        while(b!=0){
            int tmp=a^b;
            b=((unsigned int)a&b)<<1;
            a=tmp;
        }
        return a;
    }
};
```