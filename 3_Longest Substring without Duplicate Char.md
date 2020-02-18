# Leetcode 3 - Longest Substring without Duplicate Char

## Initial Idea
Sliding window + hashmap, use hashmap to record the index of char last appears. If it hasn't appeared before or the index is out of the scope of the substring currently considered, then update the new index of this char to hashmap, else move the left boundary so that the old one is excluded from the substring.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        dic={}
        left,res=0,0
        for right,val in enumerate(s):
            if val not in dic or dic[val]<left:
                res=max(res,right-left+1)
            else:
                left=dic[val]+1
            dic[val]=right
        return res
```

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        std::unordered_map<char,int> hashmap;
        int left=0;
        int res=0;
        for(int right=0;right<s.size();right++){
            if(hashmap.find(s[right])==hashmap.end()||hashmap[s[right]]<left){
                res=max(res,right-left+1);
            }else{
                left=hashmap[s[right]]+1;
            }
            hashmap[s[right]]=right;
        }
        return res;
    }
};
```