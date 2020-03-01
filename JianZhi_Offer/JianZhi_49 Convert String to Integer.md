# JianZhi 49 - Convert String to Integer

https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/

## Initial Idea
```c++
class Solution {
public:
    int strToInt(string str) {
        if(str.size()==0)
            return 0;
        int nonSpaceIndex=0;
        while(str[nonSpaceIndex]==' ')++nonSpaceIndex;
        bool negative=false;
        int digitBegin=0;
        if(str[nonSpaceIndex]=='+'){
            digitBegin=nonSpaceIndex+1;
        }else if(str[nonSpaceIndex]=='-'){
            digitBegin=nonSpaceIndex+1;
            negative=true;
        }else if(str[nonSpaceIndex]<'0'||str[nonSpaceIndex]>'9'){
            return 0;
        }else{
            digitBegin=nonSpaceIndex;
        }
        int digitEnd=digitBegin;
        while(str[digitBegin]=='0') ++digitBegin;
        while(str[digitEnd]>='0'&&str[digitEnd]<='9') ++digitEnd;
        if(digitEnd-digitBegin>11)
            return negative?-2147483648:2147483647;
        long long res=0;
        long long cnt=1;
        for(int i=digitEnd-1;i>=digitBegin;--i){
            res+=cnt*(str[i]-'0');
            if(res>=2147483648){
                res=negative?2147483648:2147483647;
                break;
            }
            cnt*=10;
        }
        if(negative)
            return -1*res;
        else
            return res;
    }
};
```

## Improvement
No need to iterate from the back to front to obtain the number. res=res*10+str[i]-'0' can do that.
```c++
class Solution {
public:
    int myAtoi(string str) {
        if(str.empty())
            return 0;
        int i=0,sign=1;
        long res=0;
        int maxInt=(~(unsigned int)0)>>1;
        int minInt=1<<31;
        while(str[i]==' ')++i;
        if(str[i]=='-')
            sign=-1;
        if(str[i]=='+'||str[i]=='-')
            ++i;
        for(;i<str.size();++i){
            if(str[i]<'0'||str[i]>'9')  //If it's not a number char, end the loop. (this also include the case where the first non space number is non number char, then it directly return res=0)
                break;
            res=res*10+(str[i]-'0');
            if((sign>0 && res>maxInt)||(sign<0 && -res<minInt)){
                res=(sign>0)?maxInt:minInt;
                return res;
            }
        }
        return (sign>0)?res:-res;
    }
};
```