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