# JianZhi 54 - The First Unduplicate Number

## Initial Idea
Use hashmap to store the number of time each number appears, use a vector to store all characters appear in the order they appear. Eventually, go through the vector and find the first char that only appears once.

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        std::vector<char> candidates;
        std::unordered_map<char,int> appearedMap;
        for(int i=0;i<s.size();++i){
            if(appearedMap.find(s[i])==appearedMap.end()){
                appearedMap[s[i]]=1;
                candidates.push_back(s[i]);
            }else{
                appearedMap[s[i]]++;
            }
        }
        for(auto& iter:candidates){
            if(appearedMap[iter]==1)
                return iter;
        }
        return ' ';
    }
};
```

## Others' Idea 1
Simply go through the string again rather than using vector to store them, but this may be slower in some extremely long string case and there are many duplicates in the front and the target is in the very back.
```c++
class Solution {
public:
    char firstUniqChar(string s) {
        std::unordered_map<char,int> appearedMap;
        for(auto& chara:s)
            appearedMap[chara]++;
        for(auto& chara:s){
            if(appearedMap[chara]==1)
                return chara;
        }
        return ' ';
    }
};
``` 