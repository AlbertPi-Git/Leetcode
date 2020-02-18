# JianZhi 40 - Find Numbers that Appear Twice

## Initial Idea
Hashmap, time complexity O(N), space complexity O(N).

```c++
class Solution {
public:
    void FindNumsAppearOnce(std::vector<int> data,int* num1,int *num2) {
        std::unordered_map<int,int> dic;
        for(auto iter:data){
            if(dic.find(iter)==dic.end()){
                dic[iter]=1;
            }else{
                dic[iter]+=1;
            }
        }
        std::vector<int> res;
        for(auto iter:dic){
            std::cout<<iter.first<<" "<<iter.second<<std::endl;
            if(iter.second==1)
                res.push_back(iter.first);
        }
        *num1=res.front();
        *num2=res.back();
    }
};
```

## Others' Idea 1
Using the property of XOR (a^b^c=a^c^b=b^c^a and a^a=0), time complexity O(N), space complexity O(1).
```c++
class Solution {
public:
    void FindNumsAppearOnce(std::vector<int> data,int* num1,int *num2) {
        int xorRes=0;
        for(int i=0;i<data.size();i++){
            xorRes^=data[i];
        }
        int firstBit1Index=getFirstBit1Index(xorRes);
        *num1=*num2=0;
        for(auto iter:data){
            if(checkBit(iter,firstBit1Index)){
                *num1^=iter;
            }else{
                *num2^=iter;
            }
        }
    }

    int getFirstBit1Index(int num){
        int mask=1;
        int index=1;
        while(0==(mask&num)){
            mask=mask<<1;
            index+=1;
        }
        return index;
    }

    int checkBit(int num, int index){
        int mask=1;
        for(int i=1;i<index;i++)
            mask=mask<<1;
        if((mask&num)>0){
            return 1;
        }else
            return 0;

    }
};
```