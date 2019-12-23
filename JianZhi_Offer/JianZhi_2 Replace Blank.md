# JianZhi_2 Replace Blank

## Initial idea
Can simply use replace function in python, it's too easy. So use C++ here.

```c++
class Solution {
public:
	void replaceSpace(char *str,int length) {
        int cnt=0;
        for(int i=0;i<length;i++){
            if(str[i]==' ')
                cnt++;
        }
        char* res=new char [length+2*cnt];
        int i=0;
        int j=0;
        while(i<length){
            if(!(str[i]==' ')){
                res[j++]=str[i++];
            }else{
                res[j++]='%';
                res[j++]='2';
                res[j++]='0';
                i++;
            }
        }
        memcpy(str,res,length+2*cnt);
	}
};
```

My C++ is so rusty.., the input parameter is a copy of the address that pointer points to. So need to put the result in that address to return modified string. 'str=res' doesn't work since it just makes the copy the that pointer point to the result but doesn't modify the original one. If the input is 'char** str', then '*str=res' will work since it modifies the original pointer.