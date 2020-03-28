# Leetcode 673 - Num of Longest Increasing Subsequence

## Initial Idea
Based on O(N^2) method in 300, and use another vector to record num of subsequence.
```c++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        if(nums.empty())
            return 0;
        std::vector<int> seqLen(nums.size(),1);
        std::vector<int> seqNum(nums.size(),1);
        std::pair<int,int> res=std::make_pair(1,1);
        for(int i=1;i<nums.size();++i){
            for(int j=0;j<i;++j){
                if(nums[i]>nums[j]){    //qualified for appending
                    if(seqLen[j]+1>seqLen[i]){  //if the sequence is longer than current one, then replace the length and number
                        seqLen[i]=seqLen[j]+1;
                        seqNum[i]=seqNum[j];
                    }else if(seqLen[j]+1==seqLen[i]){   //if just equal, then merge the number
                        seqNum[i]+=seqNum[j];
                    }
                }
            }
            if(seqLen[i]>res.first){    //if the new length is greater than current max, then we need to replace it and also update the num
                res.first=seqLen[i];
                res.second=seqNum[i];
            }else if(seqLen[i]==res.first){ //if the new length is equal to current max, then we just add this number to current max sequence number.
                res.second+=seqNum[i];
            }
        }
        return res.second;
    }
};
```