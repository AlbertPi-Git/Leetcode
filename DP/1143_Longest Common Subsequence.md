# Leetcode 1143 - Longest Common Subsequence

## Initial Idea
Two dimension DP. Let dp[i][j] holds the length of common subsequence of first i char of text1 and first j char of text2. Transition equation is:

if text1[i-1]==text2[j-1], then dp[i][j]=d[i-1][j-1]+1

else dp[i][j]=max(dp[i-1][j],dp[i][j-1])

```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int len1=text1.size();
        int len2=text2.size();
        if(len1==0||len2==0)
            return 0;
        std::vector<std::vector<int>> dp(len1+1,std::vector<int>(len2+1,0));    //Better use int array dp[][], vector is slower and takes more memory
        for(int i=0;i<len1+1;++i)
            dp[i][0]=0;
        for(int j=0;j<len2+1;++j)
            dp[0][j]=0;

        for(int i=1;i<=len1;++i){
            for(int j=1;j<=len2;++j){
                if(text1[i-1]==text2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }else{
                    dp[i][j]=std::max(dp[i-1][j],dp[i][j-1]);
                }
            }          
        }

        return dp.back().back();
    }
};
```