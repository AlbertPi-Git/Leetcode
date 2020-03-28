# Longest Concatenate Increasing String

定义上升字符串，s[i]≥s[i−1],比如aaa，abc是，acb不是；
给n个上升字符串，选择任意个拼起来，问能拼出来的最长上升字符串长度；

## Initial (and others' Idea)
This is like the mixture of merge intervals and longest increasing subsequence. Firstly, we sort all increasing substring according to their first characters (like what is done in merging intervals). Then Define the dp vector and dp[i] holds the length of the increasing subsequence of all first i+1 substrings (treat each substring as a integer in longest increasing subsequence) and also this subsequence must ends with substring strs[i] like in LC300. Then the max element of dp vector is the result.

There isn't this problem in LC, so the code isn't thoroughly tested, which means the correctness is not guaranteed.
```c++
int IncreasingStringSubSeqLen(std::vector<std::string>& strs){
    if(strs.empty())
        return 0;
    std::sort(strs.begin(),strs.end());
    std::vector<int> dp(strs.size(),0);     //dp[i] holds the length of substring that ends with strs[i]
    dp[0]=strs[0].size();
    for(int i=1;i<strs.size();++i){
        for(int j=0;j<i;++j){
            if(strs[i].front()>=strs[j].back()){
                dp[i]=std::max(dp[i],dp[j]+(int) strs[i].size());
            }
        }
    }
    return *std::max_element(dp.begin(),dp.end());

}
```
