# Leetcode 70 - Climb Stairs

## Initial Idea
Classical 1dim DP method
```c++
class Solution {
public:
    int climbStairs(int n) {
        std::vector<int> dp(n+1,0);
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=n;++i){
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
};
```

## Others' Idea 1
Current state only related with previous two states, so only need three integers.
```c++
class Solution {
public:
    int climbStairs(int n) {
        int dp_m2=1,dp_m1=1;
        int dp_cur=0;
        for(int i=2;i<=n;++i){
            dp_cur=dp_m1+dp_m2;
            dp_m2=dp_m1;
            dp_m1=dp_cur;
        }
        return n>1?dp_cur:1;
    }
};
```