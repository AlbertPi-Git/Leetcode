# JianZhi_37 - Count Number in Sorted Array

## Initial Idea
Binary search to determine whether there is target number. If there is, then expand left and right to find the boundary.

Python
```python
class Solution:
    def GetNumberOfK(self, data, k):
        # write code here
        left,right=0,len(data)-1
        find=False
        while left<=right:
            mid=(left+right)//2
            if data[mid]==k:
                find=True
                break
            elif data[mid]<k:
                left=mid+1
            else:
                right=mid-1 
        if find:
            left,right=mid,mid
            while left>=0 and data[left]==k:
                left-=1
            while right<len(data) and data[right]==k:
                right+=1
            return right-left-1
        else:
            return 0
```

C++
```c++
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        int left=0;
        int right=data.size()-1;
        int mid=0;
        bool find=false;
        while(left<=right){
            mid=(left+right)/2;
            if(data[mid]==k){
                find=true;
                break;
            }else if(data[mid]<k){
                left=mid+1;
            }else{
                right=mid-1;
            }
        }
        if(find){
            for(left=mid;left>=0&&data[left]==k;left--);
            for(right=mid;right<data.size()&&data[right]==k;right++);
            return right-left-1;
        }else{
            return 0;
        }
    }
};
```