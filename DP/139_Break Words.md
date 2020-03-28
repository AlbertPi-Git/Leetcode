# Leetcode 139 - Break Words

## Initial (Others') Idea
DP. Use dp[i] to indicate whether the first i characters of the string can be constructed from the wordDict. To get the value of dp[i], we can split the first i chars into two substrings, [0,j) and [j,i). We can directly know whether [0,j) can be constructed from the already known dp[j], so we only need to search whether [j,i) is in the dict.
```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        std::unordered_set<std::string> wordSet(wordDict.begin(),wordDict.end());
        std::vector<bool> dp(s.size()+1,false);
        dp[0]=true;
        for(int i=1;i<=s.size();++i){
            for(int j=0;j<i;++j){
                if(dp[j]&&(wordSet.find(s.substr(j,i-j))!=wordSet.end())){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp.back();
    }
};
```

## Optimization
Since the [j,i) substring must be a word in the dict, so i-j shouldn't be greater than the maximum length of words in the dict.  Thus, we can reduce the searching range of j by find the max length of words in dict in advance.
```c++
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        std::unordered_set<std::string> wordSet(wordDict.begin(),wordDict.end());
        std::vector<bool> dp(s.size()+1,false);
        dp[0]=true;
        int maxWordLen=0;
        for(auto& word: wordDict){
            maxWordLen=std::max(maxWordLen,(int)word.size());
        }
        for(int i=1;i<=s.size();++i){
            for(int j=std::max(0,i-maxWordLen);j<i;++j){
                if(dp[j]&&(wordSet.find(s.substr(j,i-j))!=wordSet.end())){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp.back();
    }
};
```