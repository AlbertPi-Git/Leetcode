# Leetcode 746 - Climb Stairs with Min Cost

## Initial Idea
In place DP on cost vector. Be careful the top of the stair isn't the last element of the cost vector, so need to append a 0 to cost before DP as the top position.
```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        cost.push_back(0);
        for(int i=2;i<cost.size();++i){
            cost[i]=std::min(cost[i-1],cost[i-2])+cost[i];
        }
        return cost.back();
    }
};
```