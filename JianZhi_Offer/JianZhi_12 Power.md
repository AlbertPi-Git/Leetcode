# JianZhi_12 Power

## Initial idea
Simple implementation.
```c++
class Solution {
public:
    double Power(double base, int exponent) {
        double res=1;
        bool negaExpo=(exponent<0);
        exponent=abs(exponent);
        for(int i=0;i<exponent;i++){
            res=res*base;
        }
        if(negaExpo){
            return 1/res;
        }else{
            return res;
        }
    }    
};
```