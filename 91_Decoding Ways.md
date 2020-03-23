# Leetcode 91 - Decoding Ways

## Initial Idea
DP, f(k)=f(k-1)+f(k-2). But '0' in the string will cause many special cases.
```python
class Solution:
    def numDecodings(self, s: str) -> int:
        if len(s)==0:
            return 0
        if len(s)==1:
            if s[0]=='0':
                return 0
            else:
                return 1
        if s[0]=='0':
            return 0
        dp=[0]*len(s)
        dp[0]=1
        if s[1]=='0':
            dp[1]=int(int(s[0:2])<27)
        else:
            dp[1]=2 if int(s[0:2])<27 else 1
        for i in range(2,len(s)):
            if s[i]=='0':
                if s[i-1]=='0' or int(s[i-1:i+1])>26:
                    return 0
                else:
                    dp[i]=dp[i-2]
            else:
                if s[i-1]=='0':
                    dp[i]=dp[i-1]
                else:
                    if int(s[i-1:i+1])<27:
                        dp[i]=dp[i-1]+dp[i-2]
                    else:
                        dp[i]=dp[i-1]
        return dp[-1]
```

## Others' Idea 1
Deal with 1 digit and 2 digits scenarios separately.

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        dp=[0]*len(s)
        dp[0]=1 if s[0]!='0' else 0
        for i in range(1,len(s)):
            if s[i]=='0':       # Deal with 1 digit scenario
                dp[i]=0
            else:
                dp[i]=dp[i-1]
            
            if s[i-1]!='0' and int(s[i-1:i+1])<27:      # Deal with 2 digit scenario
                if i==1:
                    dp[i]+=1
                else:
                    dp[i]+=dp[i-2]
        return dp[-1]
```