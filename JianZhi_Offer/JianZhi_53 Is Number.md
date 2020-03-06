# JianZhi 53 - Is Number

## Others' Idea 1
Eliminate the space before and after the first and last non-space char. Then find the E/e, then check the base part and exponent part separately.

For base part, it can only contain at least one numbers, at most one '.', at most one '+/-' (and it must locate at the beginning). Other characters are prohibited.

For exponent part, it can only contain at least one number, at most one '+/-' at the beginning. Other characters are prohibited.

```c++
class Solution {
public:
    bool isNumber(std::string s) {
        int begin,end;
        for(begin=0;s[begin]==' ';++begin);
        for(end=s.size()-1;s[end]==' ';--end);
        s=s.substr(begin,end-begin+1);
        for(int i=0;i<s.size();++i){
            if(s[i]=='e'||s[i]=='E')
                return checkBase(s.substr(0,i))&&checkExponent(s.substr(i+1,s.size()-i-1));
        }
        return checkBase(s);
            
    }
    bool checkBase(std::string s){
        int signCnt=0,dotCnt=0;
        for(int i=0;i<s.size();++i){
            if(s[i]>='0'&&s[i]<='9'){
				continue;
            }else if(s[i]=='+'||s[i]=='-'){
                if(i!=0)
                    return false;
                signCnt++;
            }else if(s[i]=='.'){
                if(dotCnt>0)
                    return false;
                dotCnt++;
            }else{
				return false;
			}
        }
        if(s.size()==0||dotCnt+signCnt==s.size())
            return false;
        else
            return true;
    }
    bool checkExponent(std::string s){
        int signCnt=0;
        for(int i=0;i<s.size();++i){
            if(s[i]>='0'&&s[i]<='9'){
				continue;
            }else if(s[i]=='+'||s[i]=='-'){
                if(i!=0)
                    return false;
                signCnt++;
            }else{
                return false;
            }
        }
        if(s.size()==0||signCnt==s.size())
            return false;
        else
            return true;
    }
};
```