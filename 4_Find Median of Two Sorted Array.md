# Leetcode 4 - Find Median of Two Sorted Array

## Initial Idea
Like merge sort, two ptr, O(M+N) time, O(1) space. Pretty lengthy because of considering even length and odd length separately.
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int totalLen=nums1.size()+nums2.size();
        int mid=(totalLen-1)/2;
        int cnt=0;
        int i=0,j=0;
        double res=0;
        if(totalLen%2==0){
            while(i<nums1.size()&&j<nums2.size()){
                if(nums1[i]<=nums2[j]){
                    if(cnt==mid||cnt==mid+1){
                        res+=nums1[i];
                    }
                    ++i;
                }else{
                    if(cnt==mid||cnt==mid+1){
                        res+=nums2[j];
                    }
                    ++j;
                }
                if(cnt==mid+1)
                    return res/2;
                ++cnt;
            }
            if(i<nums1.size()){
                while(cnt<=mid+1){
                    if(cnt==mid||cnt==mid+1){
                        res+=nums1[i];
                    }
                    ++cnt;
                    ++i;
                }
                return res/2;
            }else{
                while(cnt<=mid+1){
                    if(cnt==mid||cnt==mid+1){
                        res+=nums2[j];
                    }
                    ++cnt;
                    ++j;
                }
                return res/2;
            }
        }else{
            while(i<nums1.size()&&j<nums2.size()){
                if(nums1[i]<=nums2[j]){
                    if(cnt==mid){
                        res+=nums1[i];
                        return res;
                    }
                    ++i;
                }else{
                    if(cnt==mid){
                        res+=nums2[j];
                        return res;
                    }
                    ++j;
                }
                ++cnt;
            }
            if(i<nums1.size()){
                while(cnt!=mid){
                    ++cnt;
                    ++i;
                }
                return nums1[i];
            }else{
                while(cnt!=mid){
                    ++cnt;
                    ++j;
                }
                return nums2[j];
            }
        }
    }
};
```

## Improvement according to theirs' idea
Just use two mid index, mid1 and mid2. If the total length is odd, they are just the same. So we only need to differentiate odd and even case when we eventually return the res.
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int totalLen=nums1.size()+nums2.size();
        int mid1=(totalLen-1)/2;
        int mid2=(totalLen)/2;
        int cnt=0;
        int i=0,j=0;
        double res=0;

        while(i<nums1.size()&&j<nums2.size()){
            if(nums1[i]<=nums2[j]){
                if(cnt==mid1||cnt==mid2){
                    res+=nums1[i];
                }
                ++i;
            }else{
                if(cnt==mid1||cnt==mid2){
                    res+=nums2[j];
                }
                ++j;
            }
            if(cnt==mid2)
                return mid1==mid2?res:res/2;
            ++cnt;
        }
        if(i<nums1.size()){
            while(cnt<=mid2){
                if(cnt==mid1||cnt==mid2){
                    res+=nums1[i];
                }
                ++cnt;
                ++i;
            }
            return mid1==mid2?res:res/2;
        }else{
            while(cnt<=mid2){
                if(cnt==mid1||cnt==mid2){
                    res+=nums2[j];
                }
                ++cnt;
                ++j;
            }
            return mid1==mid2?res:res/2;
        }
        return mid1==mid2?res:res/2;
    }
};
```

## Others' Idea 1
Since at most one array will reach the end when find the median, so no need to deal with the 
```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int totalLen=nums1.size()+nums2.size();
        int mid1=(totalLen-1)/2;
        int mid2=(totalLen)/2;
        int cnt=0;
        int i=0,j=0;
        double res=0;

        for(;cnt<=mid2;++cnt){
            if(j>=nums2.size()||(i<nums1.size()&&nums1[i]<=nums2[j])){
                if(cnt==mid1||cnt==mid2)
                    res+=nums1[i];
                ++i;
            }else{
                if(cnt==mid1||cnt==mid2)
                    res+=nums2[j];
                ++j;
            }
        }
        return mid1==mid2?res:res/2;
    }
};
```