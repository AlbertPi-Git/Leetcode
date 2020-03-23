# Leetcode 63 - Unique Path II

## Initial Idea
DP
```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if len(obstacleGrid)==0:
            return 0
        if len(obstacleGrid[0])==0:
            return 1
        dp=[[0]*len(obstacleGrid[0]) for _ in range(len(obstacleGrid))]
        dp[0][0]=1
        for i in range(len(dp)):
            for j in range(len(dp[0])):
                if obstacleGrid[i][j]==1:
                    dp[i][j]=0
                    continue
                if i==0 and j==0:
                    continue
                elif i==0:
                    dp[i][j]=dp[i][j-1]
                elif j==0:
                    dp[i][j]=dp[i-1][j]
                else:
                    dp[i][j]=dp[i-1][j]+dp[i][j-1]
        return dp[-1][-1]
```

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        if(obstacleGrid.size()==0)
            return 0;
        if(obstacleGrid[0].size()==0)
            return 1;
        std::vector<std::vector<long long>> dp;
        for(int i=0;i<obstacleGrid.size();i++){
            std::vector<long long> line(obstacleGrid[0].size(),0);
            dp.push_back(line);
        }
        for(int i=0;i<obstacleGrid.size();i++){
            for(int j=0;j<obstacleGrid[0].size();j++){
                if(obstacleGrid[i][j]==1){
                    dp[i][j]=0;
                    continue;
                }
                if(i==0&&j==0)
                    dp[i][j]=1;
                else if(i==0)
                    dp[i][j]=dp[i][j-1];
                else if(j==0)
                    dp[i][j]=dp[i-1][j];
                else
                    dp[i][j]=dp[i][j-1]+dp[i-1][j];
            }
        }
        return (dp.back()).back();
    }
};
```