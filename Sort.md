# Sort algorithms

## Bubble sort
Bubble N-1 times (outer loop) since the last one doesn't need to compare with others. Each bubble iteration has N-i-1 comparisons. 

Time complexity O(N^2), space complexity O(1) (In-place sort, only use tmp variable for exchange numbers)
```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        int n=nums.size();
        for(int i=0;i<n-1;++i){
            for(int j=0;j<n-i-1;++j){
                if(nums[j]>nums[j+1]){
                    swap(nums[j],nums[j+1]);
                }
            }
        }
        return nums;
    }
};
```

## Insert Sort
Use another result container and keep it as sorted, go through the input vector and binary search the proper place in result vector to insert the number.

Time complexity O(N^2) (insert in vector takes O(N) to move elements behind it), space complexity O(N) (additional result container vector).
```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        int n=nums.size();
        vector<int> res;
        for(auto& num:nums){
            BinSearchAndInsert(res,num);
        }
        return res;
    }

    void BinSearchAndInsert(vector<int>& nums,int target){
        int left=0,right=nums.size()-1;
        while(left<=right){
            int mid=(left+right)/2;
            if(nums[mid]==target){
                nums.insert(nums.begin()+mid,target);
                return;
            }else if(nums[mid]>target){
                right=mid-1;
            }else{
                left=mid+1;
            }
        }
        if(min(left,right)<0)
            nums.insert(nums.begin(),target);
        else
            nums.insert(nums.begin()+max(left,right),target);
    }
};
```

## Quick Sort
Recursively solve sub-problems in a smaller scale. Pick the mid one as pivot, then swap it with the element of the left side. Then go through the array from two sides, find and exchange the reverse nums[i],nums[j] pair until i==j. Then pivot should be in the i th position, so swap nums[left] and nums[i]. Now elements on the left side of pivot are all smaller than pivot, and elements on the right side are all larger than pivot. Finally, recursively sort the left subarray and right subarray.  

Time complexity: average and best O(NlogN), worst O(N^2). Space complexity: best O(logN), worst O(N) stack space.

```c++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        quickSort(nums,0,nums.size()-1);
        return nums;        
    }
    void quickSort(vector<int>&nums,int left,int right){
        if(left>=right)
            return;
        int i=left,j=right,mid=(left+right)/2;
        int pivot=nums[mid];
        swap(nums[mid],nums[i]);
        while(i<j){
            while(nums[j]>=pivot&&i<j)--j;      // If place to pivot at the left side, then must start search from right side. And vice versa
            while(nums[i]<=pivot&&i<j)++i;
            swap(nums[i],nums[j]);
        }
        swap(nums[left],nums[i]);
        mid=i;
        quickSort(nums,left,mid-1);
        quickSort(nums,mid+1,right);
    }

};
```

## Merge Sort
Recursively divide big array into sub arrays that only have one or two elements. For one element sub array no need to sort, for two element sub array, only need to swap to achieve sort. Then Merge sub array together to achieve sorting of original array. 

Non-in-place merge version. Time complexity O(NlogN), space complexity O(N).
```c++
class Solution {
public:
    std::vector<int> sortArray(std::vector<int>& nums) {
        mergeSort(nums,0,nums.size()-1);
        return nums;        
    }
    void mergeSort(std::vector<int>&nums,int left,int right){
        if(left==right)
            return;
        if(left+1==right){
            if(nums[left]>nums[right])
                swap(nums[left],nums[right]);
            return;
        }
        int mid=(left+right)/2;
        mergeSort(nums,left,mid);
        mergeSort(nums,mid+1,right);
        
        //Merge
        int i=left,j=mid+1;
        std::vector<int> res;
        while(i<=mid&&j<=right){
            if(nums[i]<=nums[j])
                res.push_back(nums[i++]);
            else
                res.push_back(nums[j++]);
        }
        if(i>mid){
            for(;j<=right;++j)
                res.push_back(nums[j]);
        }else{
            for(;i<=mid;++i)
                res.push_back(nums[i]);
        }
        for(int i=0;i<res.size();++i){
            nums[left+i]=res[i];
        }
    }

};
```

In-place merge version. Time complexity O(N^2) (move in the merge part takes O(N^2) time), space complexity O(N).
```c++
class Solution {
public:
    std::vector<int> sortArray(std::vector<int>& nums) {
        mergeSort(nums,0,nums.size()-1);
        return nums;        
    }
    void mergeSort(std::vector<int>&nums,int left,int right){
        if(left==right)
            return;
        if(left+1==right){
            if(nums[left]>nums[right])
                swap(nums[left],nums[right]);
            return;
        }
        int mid=(left+right)/2;
        mergeSort(nums,left,mid);
        mergeSort(nums,mid+1,right);
        
        //Merge
        int i=left,j=mid+1;
        while(i<=mid&&j<=right){
            if(nums[i]>nums[j]){        //if nums[i]>nums[j], move the first subarray and put the nums[j] at the front.
                int tmp=nums[j];
                for(int k=j;k>i;--k)
                    nums[k]=nums[k-1];
                nums[i]=tmp;
                ++mid;      // very important, when move the first subarray, the mid also has to move or the merge will terminate too early.
                ++j;
            }
            ++i;
        }
    }
};
```


