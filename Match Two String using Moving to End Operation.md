# Match Two String using Moving to End Operation

给定两个等长字符串S,T。可以移动S的任意字符到其末尾。问最少移动几次可以使的S和T完全相同。不可以的话输出-1；
输入：abc
bac
输出  2（先移动a到末尾，再移动c到末尾）

## Others' Idea
Firstly, the appearance times of all chars in two strings must be the same or they can't match. Then iterate through s1 to find out which chars can match first N chars in s2 without changing the their relative orders. Count how many are skipped in s1 and those chars have to be moved to match s1 with s2. Since the moving order of those chars are not restricted, then number of those chars moving to end operations will solve that.
```c++
int MoveMatch(std::string s1,std::string s2){
    std::map<char,int> counter1;
    std::map<char,int> counter2;
    for(int i=0;i<s1.size();++i){
        counter1[s1[i]]+=1;
        counter2[s2[i]]+=1;
    }
    if(counter1!=counter2)
        return -1;
    int i=0;
    int j=0;
    int res=0;
    for(i=0;i<s1.size();++i){
        if(s1[i]==s2[j])
            j++;
        else
            res++;
    }
    return res;
}
```